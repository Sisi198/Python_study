
{

!pip install mne python-picard -q

}

  1. ! → Attached to the front when running terminal commands in Colab (indicates it is a system command, not Python code)

  2. pip install → The command used to install packages (libraries)

  3. mne → An EEG analysis library
  
  4. python-picard → An ICA algorithm package
  
  5. -q → "quiet" mode, which outputs a concise installation process

{

import mne

import numpy as np

import pandas as pd

from mne.preprocessing import ICA

}

  1. import → "Import this library and make it ready to use"

    Difference between install and import: 
    
     * pip install → "Install this feature onto the computer" (only needed once)

     * import → "Prepare the installed feature so I can use it right now" (needed every time)
  
  2. as np → We will refer to numpy by the short name np from now on (a conventional abbreviation)
  
  3. as pd → We will abbreviate pandas as pd
  
  4. from mne.preprocessing import ICA → Select and import only the ICA feature from the preprocessing module inside mne

      MNE stands for Magnetoencephalography and Electroencephalography.
      
      : It was originally a Python library built for analysing MEG (magnetoencephalography) and EEG (electroencephalography) data.


<img width="2616" height="668" alt="Screenshot 2026-08-11 at 4 17 53 pm" src="https://github.com/user-attachments/assets/4bbc703b-7524-4caf-a75c-df1dd2fbaba2" />


## Data download

{

!aws s3 sync --no-sign-request \
  s3://openneuro.org/ds006648/sub-001 \
  /content/ds006648/sub-001
  
  }


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
          : aws configure is an interactive setup. Instead of typing everything into a single line of code, running it will prompt 

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


<img width="1838" height="366" alt="Screenshot 2026-08-11 at 4 18 25 pm" src="https://github.com/user-attachments/assets/46c978b2-262d-496c-9759-ecf92754b066" />


## Data Loading


{

raw = mne.io.read_raw_eeglab(
    '/content/ds006648/sub-001/eeg/sub-001_task-readpoetry_eeg.set',
    preload=False
)

print(f"Duration: {raw.times[-1]:.1f} seconds")
print(f"Channels: {len(raw.ch_names)}")
print("Data loaded!")

}

    1. mne.io → MNE's file reading module
    
    2. read_raw_eeglab → Function that reads EEGLAB .set files
    
    3. '/content/...' → Path of the file to read
    
    4. preload=False → "Do not load into memory yet" (only read the path and basic metadata)

        preload=True → Loads the entire file (947MB) into RAM immediately → Risk of overwhelming RAM!

        preload=False → Only reads file information for now, loads actual data later → Safe!


      * The data is loaded into memory later when raw.load_data() is called. This allows you to configure preprocessing steps first and load the data only when needed.


    5. print(f"Duration: {raw.times[-1]:.1f} seconds") → 
    
      5-1/ raw.times is an array of timestamps per sample starting from 0 seconds. 
      5-2/ [-1] uses Python's negative indexing to denote last value of the array, which directly corresponds to the time point when recording ended: total recording duration.
      
      * Since the recording starts at 0 seconds, no separate subtraction is needed.
  
      5-3/ :.1f - A format specifier that neatly rounds and prints that value to one decimal place.

    6. print(f"Channels: {len(raw.ch_names)}") → The length of the channel names list = how many EEG (and other) channels exist in this recording.

    
Code Output EX:

{

Reading /content/ds006648/sub-001/eeg/sub-001_task-readpoetry_eeg.set

Duration: 6422.0 seconds

Channels: 70

Data loaded!

}

<img width="2644" height="694" alt="Screenshot 2026-08-11 at 4 19 37 pm" src="https://github.com/user-attachments/assets/2357ab04-281a-4a13-83d2-55c795c5a3ce" />


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


<img width="1764" height="700" alt="Screenshot 2026-08-11 at 4 38 08 pm" src="https://github.com/user-attachments/assets/70e27944-e387-4589-a769-3c4d15495f43" />

<img width="1878" height="798" alt="Screenshot 2026-08-11 at 4 38 19 pm" src="https://github.com/user-attachments/assets/d50d3e10-a6ee-40f3-9fbe-1edfab09c03f" /># EEG data Python code study



# ICA


{

raw_short = raw.copy().crop(tmax=min(3000, raw.times[-1]))

ica = ICA(n_components=63, method='picard', random_state=42, verbose=False)

ica.fit(raw_short, verbose=False)

}

  1. raw_short = raw.copy().crop(tmax=min(3000, raw.times[-1]))

    * raw.copy() → Copies the original data (leaves the original intact)

    * .crop(tmax=...) → Crops the data up to a specific time point

    * min(3000, raw.times[-1]) → Selects the smaller value between 3000 seconds and the total duration of the data. This acts as a safety measure in case a subject's dataset is shorter than 3000 seconds.

  2. ica = ICA(n_components=63, method='picard', random_state=42, verbose=False)

    * ICA() → Creates an ICA object (configures settings; does not execute yet)

    * n_components=63 → Decomposes into 63 components (because rank becomes 63 following average referencing)
    
    * method='picard' → Uses the Picard algorithm (faster than runica)
    
    * random_state=42 → Fixes the random seed so that identical results are reproduced every time

      → ICA internally utilises random numbers during calculation. Because it involves randomness, results could vary slightly every time it is executed.

      * Setting random_state=42:

        Guarantees the exact same result every time you run it.
        
        The number 42 has no special mathematical meaning; it is simply a commonly used convention. 
            
    * verbose=False → Suppresses output

3. ica.fit(raw_short, verbose=False)

    * ica.fit() → Starts the actual ICA fitting/training!
    
    * raw_short → Fits using the 3000-second cropped dataset
  

<img width="2596" height="540" alt="Screenshot 2026-08-11 at 4 39 18 pm" src="https://github.com/user-attachments/assets/0fe07c73-19a1-4947-a9a0-2c6c7bb46ef2" />


  
## Code For ICA in Actual Research Settings (Sufficient RAM)

{

ica = ICA(n_components=63, method='picard', random_state=42)

ica.fit(raw) 

}



# Automatic Artifact Classification and Removal via ICLabel

{ 

from mne_icalabel import label_components

ic_labels = label_components(raw_short, ica, method='iclabel')

labels = ic_labels['labels']

proba = ic_labels['y_pred_proba']

exclude = [i for i, label in enumerate(labels)
           if label not in ['brain', 'other']
           and proba[i].max() > 0.9]

ica.exclude = exclude

ica.apply(raw)

}

  1. from mne_icalabel import label_components

      * mne_icalabel → Dedicated library for ICLabel (requires separate installation alongside MNE)
      * label_components → Function that classifies what each ICA component represents


  2. ic_labels = label_components(raw_short, ica, method='iclabel')

      * raw_short → The 3,000-second cropped dataset used earlier (must match the data on which ICA was fitted)       
      * ica → The fitted ICA object
      * method='iclabel' → Classify components using the ICLabel model
    
  3. labels = ic_labels['labels']
  4. proba = ic_labels['y_pred_proba']

    * labels → List of component classification labels (e.g., ['eye blink', 'brain', 'muscle artifact', ...])
    * proba → Probability values for each label (e.g., 99% probability for eye blink, 1% for brain)

  5. exclude = [i for i, label in enumerate(labels)
           if label not in ['brain', 'other']
           and proba[i].max() > 0.9]

    * enumerate(labels) → Returns pairs of indices and labels (e.g., (0, 'eye blink'), (1, 'brain'))
    * label not in ['brain', 'other'] → Retains only non-brain, non-other artifacts (eye blink, muscle, channel noise, etc.)
    * proba[i].max() > 0.9 → Ensures only components with classification probability over 90% are flagged for removal


  6. ica.exclude = exclude
  7. ica.apply(raw)

    * ica.exclude = exclude → Flags the selected indices as targets for removal
    * ica.apply(raw) → Applies the ICA component subtraction across the entire dataset (the full 6,422-second dataset, not just the 3,000-second subset)


<img width="1458" height="452" alt="Screenshot 2026-08-11 at 4 49 54 pm" src="https://github.com/user-attachments/assets/ef4f2d65-5014-471a-885b-05179fd85432" />


# epoching 

{

events, event_id = mne.events_from_annotations(raw)

epochs = mne.Epochs(
    raw,
    events,
    event_id={'stimulus': 2},
    tmin=-4.0,
    tmax=11.0,
    baseline=(-4.0, 0),
    preload=True,
    verbose=False
)

}

  1. events, event_id = mne.events_from_annotations(raw)

     * mne.events_from_annotations() → Extracts event annotations embedded within the raw data
     * events → Event array containing timestamps and event codes
     * event_id → Dictionary mapping original annotation descriptions to internal MNE integer IDs (e.g., {'65282': 2, '65281': 1, ...})

  2. epochs = mne.Epochs(
    raw,                       : Raw continuous data
    events,                    : Extracted event matrix
    event_id={'stimulus': 2},  : Selects MNE ID 2 (originally '65282')
    tmin=-4.0,                 : Segment start time: 4.0 seconds prior to stimulus onset
    tmax=11.0,                 : Segment end time: 11.0 seconds after stimulus onset
    baseline=(-4.0, 0),        : Baseline correction interval
    preload=True,              : Load segmented epochs into memory immediately
    verbose=False              : Suppress execution logs
)

      * event_id={'stimulus': 2}
        * Maps MNE ID 2 (the internal integer code for annotation '65282') to the human-readable label 'stimulus'.

      * baseline=(-4.0, 0)
        * Subtracts the mean amplitude calculated across the -4.0 s to 0 s pre-stimulus interval from the entire trial segment. Zero-centring the pre-stimulus signal isolates post-stimulus evoked dynamics.
      * preload=True
        * Unlike raw continuous recordings, segmented epoch arrays (e.g., 212 trials * 15 seconds) have a substantially lower memory footprint and can safely be loaded directly into RAM.


<img width="1440" height="290" alt="Screenshot 2026-08-11 at 4 51 36 pm" src="https://github.com/user-attachments/assets/a934a26b-91f5-4f90-8fbf-04b9f041e9f0" />

       
____

# Typical Preprocessing Pipeline in Research

## Research-grade Preprocessing Pipeline

raw = mne.io.read_raw_eeglab('sub-001.set', preload=True) _→ Load full data directly_

raw.drop_channels(exg_channels)

raw.set_montage(montage)

raw.filter(l_freq=1.0, h_freq=40.0)

raw.set_eeg_reference('average', projection=False)

## ICA on full data

ica = ICA(n_components=63, method='picard', random_state=42)

ica.fit(raw) _→ Directly on full data!_

## ICLabel & Artifact removal

ic_labels = label_components(raw, ica, method='iclabel')

ica.apply(raw)

## Epoching

epochs = mne.Epochs(raw, events, tmin=-4.0, tmax=11.0, baseline=(-4.0, 0))

_____



# Condition Separation + ERP Visualisation

{

mapping = pd.read_excel('EEGLAB_Epoch_to_PoemType.xlsx')

mapping = mapping.dropna(subset=['PoemType'])


haiku_idx = mapping[mapping['PoemType'] == 'H']['EEGLAB_Epoch'].values - 1

senryu_idx = mapping[mapping['PoemType'] == 'S']['EEGLAB_Epoch'].values - 1

control_idx = mapping[mapping['PoemType'] == 'C']['EEGLAB_Epoch'].values - 1

epochs_haiku = epochs[haiku_idx]

epochs_senryu = epochs[senryu_idx]

epochs_control = epochs[control_idx]

}

  1. mapping = pd.read_excel('EEGLAB_Epoch_to_PoemType.xlsx')

     * Reads the mapping Excel file generated from Block_1~7.xlsx using pandas.
    
  2. mapping = mapping.dropna(subset=['PoemType'])

     * dropna() → Removes rows containing NaN (missing values).

     * subset=['PoemType'] → Drops rows specifically where the PoemType column is empty (which filters out practice trials like Epochs 1 and 2).
    
  3. haiku_idx = mapping[mapping['PoemType'] == 'H']['EEGLAB_Epoch'].values - 1

     * mapping[mapping['PoemType'] == 'H'] → Selects rows where PoemType is 'H'

     * ['EEGLAB_Epoch'] → Extracts only the EEGLAB_Epoch column

     * .values → Converts the pandas Series to a NumPy array

     * -1 → Converts 1-based indexing to 0-based indexing

      WHY?

       EEGLAB_Epoch:  1,  2,  3,  4, ... 212   ← 1-based (EEGLAB convention) -1 
                     -1  -1   -1  -1      -1
       ______________________________________

       Python index:  0,  1,  2,  3, ... 211   ← 0-based (Python convention)


  4. epochs_haiku = epochs[haiku_idx]

     epochs_senryu = epochs[senryu_idx]

     epochs_control = epochs[control_idx]


    * epochs[indices] → Filters the MNE Epochs object to include only the specified indices.

    * Result: Creates 3 distinct Epochs objects containing approximately 70 trials each.


<img width="1452" height="962" alt="Screenshot 2026-08-11 at 4 56 38 pm" src="https://github.com/user-attachments/assets/422714a5-75da-48e0-a8fc-fa7a91aa75c7" />


# ERP Data Extraction

{

pz_idx = epochs_haiku.ch_names.index('Pz')

haiku_erp = epochs_haiku.average().data[pz_idx] * 1e6

senryu_erp = epochs_senryu.average().data[pz_idx] * 1e6

control_erp = epochs_control.average().data[pz_idx] * 1e6

times = epochs_haiku.times * 1000

}


  1. pz_idx = epochs_haiku.ch_names.index('Pz')

     * ch_names → List of channel names (['Fp1', 'AF7', ..., 'Pz', ...])

     * .index('Pz') → Finds the numerical index corresponding to channel 'Pz'
    
       EX) if Pz is 31st, {Pz = 31}
    
  2-4. haiku_erp = epochs_haiku.average().data[pz_idx] * 1e6 / senryu_erp = epochs_senryu.average().data[pz_idx] * 1e6 / 
control_erp = epochs_control.average().data[pz_idx] * 1e6

     * epochs_haiku.average() → Computes the mean across all epochs (creates an Evoked object)
     * .data → Extracts the underlying 2D NumPy array (channels * time points)
     * [pz_idx] → Selects only the row corresponding to the Pz channel
     * $\text{* 1e6}$ → Converts voltage units from {V- Volt} to mu{V} - microvolt (FYI, 1e6 = 1,000,000)
        * Reason to convert volts into microvolts: Raw EEG signals are small floating-point values in volts (e.g., 0.000003 V = 3 muV).
    
  5. times = epochs_haiku.times * 1000

     * epochs_haiku.times → Time array in seconds (-4.0s to 11.0s)
     * $\text* 1000$ → Converts seconds to milliseconds (ms) for standard plotting conventions
        * Reason to convert: Standard ERP latency reporting uses milliseconds.


<img width="1442" height="568" alt="Screenshot 2026-08-11 at 4 57 17 pm" src="https://github.com/user-attachments/assets/f26978be-7bc2-4c26-a6b7-9c67ba660cce" />





  
# Plotting the ERP Comparison Graph

{

fig, ax = plt.subplots(figsize=(14, 5))

ax.plot(times, haiku_erp, color='blue', label='Haiku', linewidth=1.5)

ax.plot(times, senryu_erp, color='red', label='Senryu', linewidth=1.5)

ax.plot(times, control_erp, color='green', label='Control', linewidth=1.5)

ax.axvline(x=0, color='black', linestyle='--', linewidth=1)

ax.axhline(y=0, color='gray', linestyle='-', linewidth=0.5)

ax.set_xlim(-500, 3000)

ax.set_ylim(-5, 5)

ax.set_xlabel('Time (ms)')

ax.set_ylabel('Amplitude (µV)')

ax.set_title('ERP Comparison at Pz: Haiku vs Senryu vs Control')

ax.legend()

plt.tight_layout()

plt.savefig('/content/drive/MyDrive/EEG_Study/ERP_Pz_comparison.png', dpi=150)

plt.show()

}

  1. fig, ax = plt.subplots(figsize=(14, 5))

     * plt.subplots() → Creates the figure container (fig) and axis area (ax)
     * fig → The outer figure wrapper
     * ax → The actual plot canvas
     * figsize=(14, 5) → Specifies dimensions (14 inches wide x 5 inches tall)
    
  2-4. ax.plot(times, haiku_erp, color='blue', label='Haiku', linewidth=1.5) / ax.plot(times, senryu_erp, color='red', label='Senryu', linewidth=1.5) / ax.plot(times, control_erp, color='green', label='Control', linewidth=1.5)

    * ax.plot() → Plots a line graph
    * times → x-axis values (Time in ms)
    * haiku_erp → y-axis values (Amplitude in muV)
    * color='blue' → Line color
    * label='Haiku' → Label entry for the legend
    * linewidth=1.5 → Stroke thickness

  5. ax.axvline(x=0, color='black', linestyle='--', linewidth=1)

     * axvline → Vertical reference line (ax + vertical + line)
     * x=0 → Positioned at 0 ms (stimulus onset)
     * linestyle='--' → Dashed style
       
  6. ax.axhline(y=0, color='gray', linestyle='-', linewidth=0.5)

     * axhline → Horizontal reference line (ax + horizontal + line)
     * y=0 → Positioned at 0 muV (zero-voltage baseline)
    
  7-8. ax.set_xlim(-500, 3000) / ax.set_ylim(-5, 5)

    * set_xlim → Displays time window from -500 ms to 3000 ms
    * set_ylim → Sets amplitude scale from -5 muV to +5 muV

  9-11. ax.set_xlabel('Time (ms)') / ax.set_ylabel('Amplitude (µV)') / ax.set_title('ERP Comparison at Pz: Haiku vs Senryu vs Control')

    * ax.set_xlabel : display x axis in Time
    * ax.set_ylabel : display y axis in Amplitude
    * ax.set_title : display title in 'ERP Comparison at Pz: Haiku vs Senryu vs Control'

  12. ax.legend()

      * Renders the legend using designated labels (Haiku=blue, Senryu=red, Control=green)
     
  13. plt.tight_layout()

      * Adjusts margins to avoid label overlap
     
  14. plt.savefig('/content/drive/MyDrive/EEG_Study/ERP_Pz_comparison.png', dpi=150)

      * plt.savefig() → Exports plot image to Google Drive at 150 DPI resolution
      * Path: The EEG_Study folder in Google Drive
      * dpi=150 → Resolution (higher values result in clearer images, but larger file sizes)

  15. plt.show()

      * Displays plot in the notebook output
     
<img width="1438" height="692" alt="Screenshot 2026-08-11 at 4 57 44 pm" src="https://github.com/user-attachments/assets/9b452df1-118f-4fe0-8404-a643111f615a" />


     
# Preprocessing Automation Function

## Function Declaration

{

def preprocess_subject(subject_id):

    print(f"\n{'='*50}")
    
    print(f"Processing sub-{subject_id}...")
    
    print(f"{'='*50}")

}

1. def preprocess_subject(subject_id):
   
  * def → Python keyword meaning "I am defining a function"
  * preprocess_subject → Function name (meaning preprocessing function)
  * subject_id → Input value (e.g., subject numbers like '001', '002', etc.)

2. print(f"\n{'='*50}")
   
   print(f"Processing sub-{subject_id}...")
   
   print(f"{'='*50}")

  * This is used to visually track which subject is currently being processed when running through all 18 subjects!
  * When executed, it looks like this:

    **  ==================================================

    Processing sub-001...

     ==================================================**

3.

import os

os.system(f'aws s3 sync --no-sign-request s3://openneuro.org/ds006648/sub-{subject_id} /content/ds006648/sub-{subject_id}')

  * os → Library containing operating system-related functions
  * os.system() → Runs terminal commands directly from within Python
  * f'aws s3 sync ... sub-{subject_id}' → Automatically updates the path based on subject_id:
    * If subject_id='002'→ Downloads sub-002
    * If subject_id='003'→ Downloads sub-003
   
4. 
set_file = f'/content/ds006648/sub-{subject_id}/eeg/sub-{subject_id}_task-readpoetry_eeg.set'

if not os.path.exists(set_file):

    print(f"sub-{subject_id}: .set file not found, skipping!")
    
    return None

  * os.path.exists() → to check if this file is in this path
  * if not → If the file does not exist,
    * return None → Stops the function right here and returns None (moves on to the next subject)

  * Why this is important:
    * Even if a download fails for a specific subject:
      * the entire script will not halt due to an error→ it simply skips that subject and moves on to the next one
     
<img width="972" height="218" alt="Screenshot 2026-08-11 at 4 59 48 pm" src="https://github.com/user-attachments/assets/46c9aa6b-5dd0-4930-8d19-4e507f454dab" />




### The remaining sections (preprocessing, ICA, epoching, and saving) are identical to the previous codes

{

import gc

subjects = ['001', '002', '003', ... '018']

for sub in subjects:

    epochs = preprocess_subject(sub) 
    
    del epochs  
    
    gc.collect()  

}

  * for sub in subjects → Iterates through all 18 subjects in order
  
  * preprocess_subject(sub) → Calls the function (passing '001', '002', etc. into sub)
  
  * del epochs → Deletes the processed data from RAM
  
  * gc.collect() → Garbage collector = clears unreferenced memory

<img width="1166" height="692" alt="Screenshot 2026-08-11 at 5 00 35 pm" src="https://github.com/user-attachments/assets/b85dea0d-014f-4249-8130-48b59a0c70a2" />



