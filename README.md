# EEG data Python code study

{!pip install mne python-picard -q}

  1. ! → Attached to the front when running terminal commands in Colab (indicates it is a system command, not Python code)

  2. pip install → The command used to install packages (libraries)

  3. mne → An EEG analysis library
  
  4. python-picard → An ICA algorithm package
  
  5. -q → "quiet" mode, which outputs a concise installation process

{import mne
import numpy as np
import pandas as pd
from mne.preprocessing import ICA}

  1. import → "Import this library and make it ready to use"

    Difference between install and import: 
    
     * pip install → "Install this feature onto the computer" (only needed once)

     * import → "Prepare the installed feature so I can use it right now" (needed every time)
  
  2. as np → We will refer to numpy by the short name np from now on (a conventional abbreviation)
  
  3. as pd → We will abbreviate pandas as pd
  
  4. from mne.preprocessing import ICA → Select and import only the ICA feature from the preprocessing module inside mne

      MNE stands for Magnetoencephalography and Electroencephalography.
      
      : It was originally a Python library built for analysing MEG (magnetoencephalography) and EEG (electroencephalography) data.

## Data download

{!aws s3 sync --no-sign-request \
  s3://openneuro.org/ds006648/sub-001 \
  /content/ds006648/sub-001}


    1. aws s3 sync → Synchronise (download) files from an AWS S3 bucket

      AWS S3 = A cloud storage service operated by Amazon

      OpenNeuro = A platform for sharing research data, which rents and uses AWS S3 to actually store the data
    
    2. --no-sign-request → Access public data without signing in / authenticating

       Q. How does the code change if a login is required?

        * Public data (Our current situation)
        !aws s3 sync --no-sign-request s3://bucket-address /save-path

        * When login is required
        !aws configure  # Enter AWS account key
        !aws s3 sync s3://bucket-address /save-path  
        →   --no-sign-request is omitted

       * How to use aws configure
          : aws configure is an interactive setup. Instead of typing everything into a single line of code, running it will prompt questions one by one for you to answer:

                $ aws configure
                  AWS Access Key ID: AKIAIOSFODNN7EXAMPLE        ← Type here
                  AWS Secret Access Key: wJalrXUtnFEMI/K7MDENG  ← Type here
                  Default region name: us-east-1                 ← Type here
                  Default output format: json                    ← Type here

          * Method to input all at once via code

            import os
              os.environ['AWS_ACCESS_KEY_ID'] = 'your_key'
              os.environ['AWS_SECRET_ACCESS_KEY'] = 'your_secret'
              os.environ['AWS_DEFAULT_REGION'] = 'us-east-1'

              # Then run sync
              
              !aws s3 sync s3://bucket-address /save-path
    
    3. s3://openneuro.org/ds006648/sub-001 → Source location to download from (S3 server)

        * s3:// = Storage located on AWS servers
    
    4. /content/ds006648/sub-001 → Destination to save to (inside Colab)

      * Difference between \ and /

        1.  \ is a line continuation symbol — meaning "this command is not finished yet and continues onto the next line."
        2. Windows uses \ as a path separator, but Mac, Linux, and Colab use /

    →  Copy the sub-001 data on the OpenNeuro server into the Colab environment.

## Data Loading


{
raw = mne.io.read_raw_eeglab(
    '/content/ds006648/sub-001/eeg/sub-001_task-readpoetry_eeg.set',
    preload=False
)
}

    1. mne.io → MNE's file reading module
    
    2. read_raw_eeglab → Function that reads EEGLAB .set files
    
    3. '/content/...' → Path of the file to read
    
    4. preload=False → "Do not load into memory yet" (only read the path and basic metadata)

        preload=True → Loads the entire file (947MB) into RAM immediately → Risk of overwhelming RAM!

        preload=False → Only reads file information for now, loads actual data later → Safe!


      * The data is loaded into memory later when raw.load_data() is called. This allows you to configure preprocessing steps first and load the data only when needed.


# remove EXG channel

{
exg_channels = [ch for ch in ['EXG1','EXG2','EXG3','EXG4','EXG5','EXG6','EXG7','EXG8'] if ch in raw.ch_names]
raw.drop_channels(exg_channels)
}

    
    1. exg_channels = [ch for ch in ['EXG1','EXG2','EXG3','EXG4','EXG5','EXG6','EXG7','EXG8'] if ch in raw.ch_names]
    
   * List Comprehension:

     ['EXG1', ..., 'EXG8'] → List of channel names you want to remove

     * if ch in raw.ch_names → Selects only the ones that actually exist in the data. This is because sub-001 did not have EXG5 or EXG6. Trying to remove channels that aren't there will trigger an error.

    2. raw.drop_channels(exg_channels)

     Requesting Python to actually remove the channels selected above


# Setting the Montage

{
montage = mne.channels.make_standard_montage('biosemi64')
raw.set_montage(montage, on_missing='warn')
}

    1. montage = mne.channels.make_standard_montage('biosemi64')

       * mne.channels → Channel-related module in MNE
  
       * make_standard_montage → "Create standard channel location information"
      
       *'biosemi64' → Standard electrode locations for BioSemi 64-channel equipment
        
        → # Code to check available montages
          
          {mne.channels.get_builtin_montages()}

          Commonly used ones:
          
            BioSemi 64-channel - 'biosemi64'
            BioSemi 128-channel - 'biosemi128'
            Standard 10-20 system - 'standard_1020'
            EGI 128-channel - 'GSN-HydroCel-128'

       * It means: "Load the standard electrode location information for the BioSemi 64-channel equipment."


    2. raw.set_montage(montage, on_missing='warn')

      * raw.set_montage() → Apply the location information we just created to the actual data

      * on_missing='warn' → If there are channels without location information, display a warning instead of raising an error
          → Keep processing, even if the EXG channel was not present in the montage. Still display the warning for any random scenario
    
      Q. Is it usually better to include on_missing='warn' just in case?
    
      A. 
      
      'warn': Ignores issues and proceeds → You might overlook problems later. [Development/testing]

      'raise': Immediately stops with an error if there is a problem → Allows for definitive verification. [Final analysis]

# Loading Data into Memory + Filtering

{
raw.load_data()
raw.filter(l_freq=1.0, h_freq=40.0, verbose=False)
}

  1. raw.load_data()

    * Previously, only read the file metadata using {preload=False}

    * This tells it: "Now load the actual data into RAM." - This is the exact moment when the 947MB is finally loaded into memory.

    
  2. raw.filter(l_freq=1.0, h_freq=40.0, verbose=False)

    * raw.filter() → Applies filtering

    * l_freq=1.0 → Low frequency = Removes anything below 1Hz (low-frequency drift)
    
    * h_freq=40.0 → High frequency = Removes anything above 40Hz (high-frequency noise)
    
    * verbose=False → Do not print the filtering process : When running multiple subjects automatically, long printouts for each subject get messy.

      FYI: 
      
      * When installing via pip: -q

      * pandas: same with MNE, verbose=False

      * scikit-learn (Machine Learning library): verbose=0
      
     ! verbose is MNE-specific


# Re-referencing

{
raw.set_eeg_reference('average', projection=False, verbose=False)
}

  1. raw.set_eeg_reference() : Re-configure the reference electrode for the EEG data

    Q. What was the original reference?
    
    A. When recording EEG, all signals are measured using a specific location as the "0 baseline." Voltage cannot be measured without a baseline (because voltage is always relative—"how much relative to where").

      * Original reference for dataset ds006648: EXG5, EXG6 = Electrodes attached behind the ears (mastoid); The eeg.json file stated "EEGReference": "earlobes"

  2. 'average' : Sets it to the Average Reference & adjusts the average of all 64 channels to 0

    Q. Why set the average of the 64 channels to 0?

    A. EEG signals are "relative values against a reference," not absolute voltage values.
    
    When ear-referenced: {Fz signal} = {Fz electrode voltage} - {ear electrode voltage}
    
    When average-referenced:{Fz signal} = {Fz electrode voltage} - {average voltage of all 64 channels})
    
    * Ear references can introduce bias toward the location of the ears. 
    
      → EX: channels near the ears (T7, T8) are close to the reference point, so their signals might appear smaller, while distant channels (Fz) might appear larger. Average referencing handles every channel equitably, eliminating location-based bias

  3. projection=False : True → Apply the reference later (delayed application) / False → Apply it right now, immediately

     * projection=True (Apply later):

        Saved as a "projector" object.
        
        Applied automatically later when plotting or analysing.
        
        The raw data values remain unchanged.
    
     * projection=False (Apply right now):

        Modifies the numerical values in the dataset immediately.
        
        Reflected automatically in all subsequent analyses.


     Q. Why we used False:

     A. Before running ICA, the data values themselves must already be converted to average reference. If set to True, ICA might calculate components using the un-referenced raw data, which carries risk.


GENERAL INFO.

Common types of references:

 1. Mastoid (Behind ear):	Electrodes attached to the bone behind the ears	(Usage: Clinical, BioSemi)
 2. Linked mastoid:	Average of both ears	(Usage: Traditional ERP research)
 3. Average reference: Average of all channels	(Usage: High-density EEG (64+ channels) )
 4. Nose tip:	Electrode on the tip of the nose	(Usage: Certain clinical studies)
 5. Cz:  Centre channel on top of the head	(Usage: Select research settings)


! The reference is chosen by the researcher when designing the experiment. However, in the analysis phase, converting to Average Reference is the standard approach for high-density EEG (64+ channels)


# ICA

raw_short = raw.copy().crop(tmax=min(3000, raw.times[-1]))
ica = ICA(n_components=63, method='picard', random_state=42, verbose=False)
ica.fit(raw_short, verbose=False)


     
