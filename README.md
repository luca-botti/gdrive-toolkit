# gdrive-toolkit

various tools for managing files on google drive using gdrive and csvkit.

For now there is:

- searching for id from an exact file or folder name (two algorithm bfs and dfs, no correction for multiple folders of files with the same name at the moment)
- getting the list of object in a folder (by name), possibility to filter them by folders, regular documents, google documents, or shortcuts

TODO

- return the size of all file in a folder or of a single file
- correction of duplicates while getting ids

# Installing

See [gdrive repository](https://github.com/glotlabs/gdrive) for info about installing gdrive, and run `sudo apt install csvkit` for install csv kit.

I've also created a script for building gdrive from source, and i've used it for running the program on my raspberrypi.

Do Not Run the script if you don't know what each command do.

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y # installing rust silently withount promting
source "$HOME/.cargo/env" # adding rust binaries to PATH

mkdir .gdrive
cd .gdrive/

LATEST=$(curl -Ls -o /dev/null -w %{url_effective} https://github.com/glotlabs/gdrive/releases/latest) # getting latest version code
LATEST=$(basename $LATEST)
curl -Ls -o "gdrive-$LATEST.tar.gz" https://github.com/glotlabs/gdrive/archive/refs/tags/$LATEST.tar.gz # downloading binaries
tar -xzf "gdrive-$LATEST.tar.gz" # extracting them
cd gdrive-$LATEST/ # go inside the dowloaded binaries
sudo chown -R pi .
cargo build --release # building gdrive
sudo cp target/release/gdrive /usr/local/bin # adding gdrive to PATH
cd ../..
sudo rm -r .gdrive #cleaning
```
Then follow the instruction in the [gdrive repository](https://github.com/glotlabs/gdrive) for adding the account