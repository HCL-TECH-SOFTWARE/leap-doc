# Building an image

A Domino Leap image can be built by using the open-source Domino Container utilities provided by HCL Software.

For more information on the procedure, see this [Domino Container](https://opensource.hcltechsw.com/domino-container/) article.

## Prerequisites

- A general understanding of Docker, or Podman

- An environment that is enabled with Docker, or Podman. This could be a native Linux installation or WSL on Windows.

## Procedure

1. Open a command-line terminal in an environment that is enabled with Docker or Podman.

2. Download (or clone) the domino-container repository from github.com.

3. Download the latest Domino Server binary (ex. “Domino_xx.x_Linux_English.tar”) and the Domino Leap install package (ex. “hcl.dleap-x.x.x.xx.zip”) from Flexnet or the My HCLSoftware Portal and place them into the …/domino-container/software/ directory.

4. Run the following commands:

```
cd …/domino-container/
./build.sh domino -leap
```

!!! note
    (Optional) If the built image is to be run elsewhere, use docker export command to export the image as a .tar file.


**Parent topic:** [Deploying Domino Leap in a container](dleap_deploy_to_container.md)