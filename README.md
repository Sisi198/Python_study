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



