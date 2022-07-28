# Using Polymake in MATLAB via Docker

## About Polymake and Docker ##
"[polymake](https://polymake.org/doku.php) is open source software for research in polyhedral geometry. It deals with polytopes, polyhedra and fans as well as simplicial complexes, matroids, graphs, tropical hypersurfaces, and other objects. Supported platforms include various flavors of Linux, FreeBSD and Mac OS."

## Installation ##
The following steps can be used on Windows OS to install Docker and an Archlinux distributiin with the latest Polymake version:

1. Install Docker from the following [link](https://www.docker.com/).
2. Make a temporary folder on your computer. 
3. Inside the new folder, create a Dockerfile with the following code:
```
FROM archlinux
RUN pacman -Syu --noconfirm polymake
```
This should also install the latest version of Polymake inside Archlinux.
4. Create the docker image using: 
```
docker build -t arch-docker .
```
5. In MATLAB, create a [Polymake script](https://polymake.org/doku.php/user_guide/howto/scripting) and save it as polymake_script.pl
6. Execute the Polymake script from MATLAB Command Window using:
```
!docker run --rm -v "%cd%":/app arch-docker polymake --script /app/polymake_script.pl /app
```
