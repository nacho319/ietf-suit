SUIT Hackathon at IETF103
-------------------------

Attendees:

- Hannes Tschofenig 
- Jaime Jiménez 
- Tadahiko Ito 
- Yohei Kaieda 
- Yuichi Takita 
- Dave Thaler 
- Dan Petrie
- Emmanuel Baccelli
- Henk Birkholz
- Chris Inacio
- Laurence Lundblade

Twitter: #IETFHackathon & #IETF103

Hackathon Wiki: https://trac.ietf.org/trac/ietf/meeting/wiki/103hackathon
Etherpad: https://etherpad.tools.ietf.org/p/FUIETF103
SUIT IETF101: https://gist.github.com/jaimejim/3aa9c6e85e82a353c9fa90794c856d89
SUIT IETF102: https://gist.github.com/jaimejim/82d53f97a9d011ef13c8750129b84cb1
Poster info: http://jaimejim.github.io/docs/suit_poster.pdf

## Hackathon 103 goals

We have multiple points to touch:
    - Jaime: The manifest information model has been updated and so should the example. The goal will be to have the new json manifest example and update the tools to encode, sign...
    -  Hannes: I am trying to write a bootloader for the STM32F412ZG MCU. More information about the board can be found at https://os.mbed.com/platforms/Mbed-WiFi-BLE/

    
## Toolchain Installation with Docker

Install Docker. Probably `sudo apt-get install docker` or [download](https://docs.docker.com/docker-for-mac/install/#install-and-run-docker-for-mac) and install. 

### MBED CLI

`docker pull jaim/mbed-cli`
`docker run -ti -v $(pwd):/mbed:cached jaim/mbed-cli:default`

### RIOT environment

```
docker pull riot/riotbuild
git clone https://github.com/RIOT-OS/RIOT.git
```
Then in the RIOT directory
```
make BUILD_IN_DOCKER=1 -C examples/hello-world/ BOARD=frdm-k64f
```
For this to work on Mac, you will have to remove the line below (line 112) in `makefiles/docker.inc.mk`:
        '        -v /etc/localtime:/etc/localtime:ro \'
    


### Manifest Generator

Brendan has been working on an updated version of the Python-based manifest generator. The code is availble here: 
https://github.com/ARMmbed/suit-manifest-generator

### Renesas RX231 environment

Create a new RX231 bootloader for SUIT.
Plan:
1. Create a manifest file (with cose digest for key file) for RX231.
    >  Done except for cose digest for key. The manifest file version is draft-moran-suit-manifest-03.
2. Create a bootloader program with below three steps.
    - Secure boot and, Install keys.
        > Done.
    - Check a Manifest file. ( and Check if the set of Firmware, Keyfile, and Manifest is valid.)
    - Decrypt and load a firmware file.
       > Done.

More Information about board can be found at https://www.renesas.com/sg/en/products/microcontrollers-microprocessors/rx/rx200/rx231.html

### COSE Examples

https://github.com/cose-wg/Examples


### Updating Manifest example from the draft

There have been quite a lot of changes in moran-suit-manifest https://tools.ietf.org/rfcdiff?url2=draft-moran-suit-manifest-03.txt

We take out the cddl (https://tools.ietf.org/id/draft-moran-suit-manifest-03.html#rfc.section.8)

```
brew install ruby
hash -r
gem install cddl
cddl manifest03.cddl json-generate > m03.json 
```

Note: Since the original CDDL was not correct we ignored the possibility of auto-generating a manifest file in JSON and define it manually instead. The other examples in the draft are wrong too. 
Tools needed:
    
```
pip3 install cbor
gem install cddl
```
The CBOR Diagnostic example is: https://github.com/jaimejim/suit-manifest-generator/blob/master/suit103.cbordiag


### IETF SUIT Workshop board notes / details

Processor
GPIO map

