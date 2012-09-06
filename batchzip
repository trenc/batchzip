#!/bin/sh
#
# Name: batchzip
# Description: This script zips files with same basename (ignoring the extension).
# Author: Tommy Schmucker
# Created: 2012-05-13
# Modified: 2012-05-16
# Version: 0.3
#

usage()
{
	cat << EOF

This script zips files with same basename (ignoring the extension).

usage: $0 [-h] [-r] [-d directory]

-h Show this message
-d Input directory
-r Remove original files
EOF
}

dir=`pwd`
rm_orig=0
me=`basename $0`

zip=/usr/bin/zip
rm=/bin/rm

[ -x $zip ] || { echo "No such executable: $zip"; exit 1; }
[ -x $rm ] || { echo "No such executable: $rm"; exit 1; }

while getopts "hrd:" option; do
	case $option in
		h)
			usage
			exit 1
			;;
		r)
			rm_orig=1
			;;
		d)
			dir="$OPTARG"
			;;
		?)
			usage
			exit
			;;
	esac
done

[ -d "$dir" ] || { echo "$in_dir is not a directory, exiting"; exit 1; }
dir="${dir%/}"

for this_file in "$dir"/*; do
	basename=$(basename "$this_file")
	name=${basename%.*}
	if [ ! -h "$this_file" ] && [ "$basename" != "$me" ]; then
		$zip -j "$dir"/"$name".zip $this_file
		if [ "$rm_orig" == 1 ]; then
			$rm "$this_file"; echo "$basename removed."
		fi
	fi
done
