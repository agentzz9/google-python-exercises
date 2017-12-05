#!/usr/bin/python
# Copyright 2010 Google Inc.
# Licensed under the Apache License, Version 2.0
# http://www.apache.org/licenses/LICENSE-2.0

# Google's Python Class
# http://code.google.com/edu/languages/google-python-class/

import sys
import re
import os
import shutil
import commands

"""Copy Special exercise
"""

# +++your code here+++
# Write functions and modify main() to call them

def isspecial(filename):
  match = re.search(r'\w+__\w+__\w*.\w+', filename)
  if match:
    return True
  else:
    return False


#listthem
def ListSpecialFiles(directory):
  filenames = os.listdir(directory)

  specialfilenames = []
  for filename in filenames:
    if isspecial(filename):
      specialfilenames.append(filename)
  
  for specialfilename in specialfilenames:
    path = os.path.join(directory, specialfilename)
    print os.path.abspath(path)



#copy
def copyspecialfiles(directory, target):
  filenames = os.listdir(directory)
  absolutepaths = []
  specialfilenames = []
  for filename in filenames:
    if isspecial(filename):
      specialfilenames.append(filename)
  
  for specialfilename in specialfilenames:
    path = os.path.join(directory, specialfilename)
    absolutepaths.append(os.path.abspath(path))

  target = target.lstrip('/')
  targetpath = os.path.join(directory, target)
  targetpath = os.path.abspath(targetpath)

  if not os.path.exists(targetpath):
    os.mkdir(targetpath) 

  for path in absolutepaths:
    shutil.copy(path, targetpath)
  
#zip
def zipspecialfiles(directory, zipfilename):
  filenames = os.listdir(directory)
  absolutepaths = []
  specialfilenames = []
  for filename in filenames:
    if isspecial(filename):
      specialfilenames.append(filename)
  
  for specialfilename in specialfilenames:
    path = os.path.join(directory, specialfilename)
    absolutepaths.append(os.path.abspath(path))

  cmd = 'zip' + ' ' + '-j' + ' ' + zipfilename
  for path in absolutepaths:
    cmd = cmd + ' ' + path
  
  (status, output) = commands.getstatusoutput(cmd)

  print cmd

  if status:
    sys.stderr.write('error :' + output)
    sys.exit(1)
  else:
    print 'success.'


def main():
  # This basic command line argument parsing code is provided.
  # Add code to call your functions below.

  # Make a list of command line arguments, omitting the [0] element
  # which is the script itself.
  args = sys.argv[1:]
  if not args:
    print "usage: [--todir dir][--tozip zipfile] dir [dir ...]";
    sys.exit(1)

  # todir and tozip are either set from command line
  # or left as the empty string.
  # The args array is left just containing the dirs.
  todir = ''
  if args[0] == '--todir':
    todir = args[1]
    del args[0:2]

  tozip = ''
  if args[0] == '--tozip':
    tozip = args[1]
    del args[0:2]

  if len(args) == 0:
    print "error: must specify one or more dirs"
    sys.exit(1)

  if not todir and not tozip:
    ListSpecialFiles(args[0])
  else:
    if todir:
      copyspecialfiles(args[0],todir)
    if tozip:
      zipspecialfiles(args[0],tozip)

  # +++your code here+++
  # Call your functions
  
if __name__ == "__main__":
  main()
