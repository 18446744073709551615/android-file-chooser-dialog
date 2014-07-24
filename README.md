android-file-chooser-dialog
===========================

Android file chooser, a dialog to pick a filename.

The code is taken from
http://www.scorchworks.com/Blog/simple-file-dialog-for-android-applications/
with a few added features and bug fixes.

What has changed: I needed ability to go to the root directory, but the original code did not permit
going above the sdcard mount point, and if you used a non-default start folder not on sdcard,
the code crashed in the root directory. This has been fixed.

Usage example
-------------

    public void onButtonChooseFile(View v) {
        //Create FileOpenDialog and register a callback
        SimpleFileDialog fileOpenDialog =  new SimpleFileDialog(
            MainActivity.this,
            "FileOpen..",
            new SimpleFileDialog.SimpleFileDialogListener()
            {
                @Override
                public void onChosenDir(String chosenDir) 
                {
                    // The code in this function will be executed when the dialog OK button is pushed
                    editFile.setText(chosenDir);
                }
            }
        );
        //You can change the default filename using the public variable "Default_File_Name"
        fileOpenDialog.default_file_name = editFile.getText().toString();
        fileOpenDialog.chooseFile_or_Dir(fileOpenDialog.default_file_name);
    }

And remember

    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

Dialog modes
------------

    "FileOpen" -- open an existing file
    "FileSave" -- save to a file
    "FolderChoose" -- choose a folder
    "FileOpen.." -- open an existing file, can cd .. from the starting directory
    "FileSave.." -- save to a file, can cd .. from the starting directory
    "FolderChoose.." -- choose a folder, can cd .. from the starting directory

