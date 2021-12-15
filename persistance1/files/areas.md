# Areas to think of

## Locks, and the lack thereof

- When you open a file, you specify how you plan to work with it (Read/Write/Both)
  - as well as whether to allow other processes to read or write the file while open.
- You have to be careful with this, because you could break other processes with the wrong locking settings
  -  either by keeping them from accessing the file, or
  -  by altering the file while they are accessing it.
- The same principal can work in reverse on you.
  - For instance, if you are reading a file while allowing other processes to write to the file, you could run into a situation where the file changes between reads.
  - You may also find that you are denied access to a file due to the constraints placed on it by other apps. Those other apps may not be running (or running at much lower scale) in your development environment.

## Removable (or disconnect-able) media

- Back in the day, we had to worry about floppy disks (or even zip disks, or CDs) getting ejected while we were attempting to use them.
  - While less of a worry today, it’s still a potential problem.
  - Things like USB drives, network shares, and even the occasional DVD (or even a floppy!!) could be disconnected or removed while you are accessing them.
- Worse still, you aren’t necessarily going to get a lot of notice if it is going to happen.
- You probably also don’t want to immediately fail if the device is temporarily disconnected (USB hub power issues, or network blips, for instance),
  - but rather have some retry logic.
- In addition to total failure, at least some of these devices could remain connected, but become horribly slow.
  -  This is especially true of networked devices. You may need to take this into account as well.


## Permissions

- Just because you can see (or even open) a file, doesn’t mean that you can write to it.
- File system permissions are one of the primary ways that you’ll get burned here.
- Files aren’t the only things that are secured.
  - Paths are as well, so you may not even be able to see a folder in which your file resides.
- Permissions also may be more granular than you want.
  - For instance, you might be able to read a file, or append to it, but be unable to overwrite it.
- Many systems (Linux, for example) also include an execute bit, so if you are attempting to run another program or script, this permission may get in your way as well.

## Disk issues

- Hard drives fail or develop various problems over their lifecycle.
  - This used to be more common than it is now, but it still does happen.
- It’s also possible that the hard drive may be under high utilization and simply be slow,
  - or that the file system on the disk is slow due to lack of maintenance (in file systems where this is an issue).
- These issues don’t just happen when you first open a file, as they can occur while you are reading/writing the file.
- Make sure your code is appropriately handling errors any time it is accessing the file system.

## Encodings

- Not all files are ascii.
- Not all file paths are either.
- This can burn you if you are making assumptions in your code, especially if you are in the English-speaking world, but have clients elsewhere.
- Similarly, the contents of the files may reflect a different encoding.

## Path issues

- Just because you get a file path, doesn’t mean you can use it.
- This is especially true if paths come out of config files and the like.
- It’s also a problem if the user enters a path that is too long.
  - While most modern tools can handle longer file paths, some older tools that are still in use cannot and will crash.
- Be aware that path separators are not always the same.
  - Windows uses ‘\’ and unix uses ‘/’.
- Also be aware that some characters in path strings have special meaning in things like globs, regexes, and regular old strings (escape sequences, for instance).
- Two paths that are string equal are not necessarily the same file, and two paths that are different can be the same file.
- Remember that OS’es have options for aliasing and the like.
- Be careful moving files as well.
  - A file path that is acceptable in one directory may be too long when moved to another.

## File naming issues

- Some characters can’t be used in file names.
  - For instance, windows doesn’t allow glob characters (like *, ?) to be used in file names.
- Some filenames are special.
  - For instance, you can’t use con.txt or aux.mp3.
  - This is an ancient backward compatibility thing.
- Also, watch how you treat file extensions.
  - The extension is not the first three characters after the first period…
  - Speaking of extensions, be careful to use appropriate extensions for any files that are intended to be read by humans or by other programs.
    - Some apps simply look at the extension on a file to determine what tool should open that file, so an incorrect extension can cause problems.

## Timing issues

- Many enterprise systems run anti-virus software that scans new files before allowing access to them.
  - This can mean that you can’t read a file just after it is written to disk.
-  Additionally, just because a new file is on disk doesn’t mean that it is ready for reads.
  - For instance, large files being transferred over a slow connection may take several minutes to truly be available.
- It’s also possible to see a file on the file system and have it disappear between it being found and being opened.
  - Basically, even though you are taught to check for a file’s existence before trying to open it, that’s not a perfect way to make sure the file exists, is readable, and can be accessed by you

## Integration point

- Using files as a means of communication
- This can be done over the network ie use of http or ftp
- Using a shared file system for several apps 
- Not the best way of doing things, but is still in use
