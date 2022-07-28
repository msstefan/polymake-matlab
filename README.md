# Using Polymake in MATLAB via Docker

## About Polymake and Docker ##
> [Polymake](https://polymake.org/doku.php) is open source software for research in polyhedral geometry. It deals with polytopes, polyhedra and fans as well as simplicial complexes, matroids, graphs, tropical hypersurfaces, and other objects. Supported platforms include various flavors of Linux, FreeBSD and Mac OS.

> [Docker](https://docs.docker.com/get-started/overview/) is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly.

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
5. In MATLAB, create a [Polymake script](https://polymake.org/doku.php/user_guide/howto/scripting) and save it as `polymake_script.pl`.
6. Execute the Polymake script from MATLAB Command Window using:
```
!docker run --rm -v "%cd%":/app arch-docker polymake --script /app/polymake_script.pl /app
```

## Example: printing polytope's constraints ##
Create the `polymake_script.pl` with the following code:
```
use application "polytope";
my $p = new Polytope(INEQUALITIES=>[[1,1,0],[1,0,1],[1,-1,0],[1,0,-1],[17,1,1]]);
print_constraints($p->INEQUALITIES);
```
Run this command in MATLAB Command Window:
```
!docker run --rm -v "%cd%":/app arch-docker polymake --script /app/polymake_script.pl /app
```
The following output should be produced:
```
0: x1 >= -1
1: x2 >= -1
2: -x1 >= -1
3: -x2 >= -1
4: x1 + x2 >= -17
5: 0 >= -1
```
