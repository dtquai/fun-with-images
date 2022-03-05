# Quantum Computing on Julia

FROM nvidia/cuda:11.6.0-base-ubuntu20.04

ARG JULIA_VER=1.7.2
ARG JULIA_URL=https://julialang-s3.julialang.org/bin/linux/x64/1.7
ARG JUPYTER_PW=pw
ARG USER_ID=3003

EXPOSE 8888
USER root
WORKDIR /

RUN apt-get update && apt-get install -y \
	curl tar tmux

RUN curl -LO https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && \
	bash Miniconda3-latest-Linux-x86_64.sh -p /miniconda -b && \
	rm Miniconda3-latest-Linux-x86_64.sh
ENV PATH=/miniconda/bin:${PATH}

RUN conda update -y conda && \
	conda install -y -c conda-forge jupyterlab
RUN mkdir /.local && \
	chown ${USER_ID} /.local

RUN curl -LO ${JULIA_URL}/julia-${JULIA_VER}-linux-x86_64.tar.gz && \
	tar -xf julia-${JULIA_VER}-linux-x86_64.tar.gz && \
	rm -rf julia-${JULIA_VER}-linux-x86_64.tar.gz && \
	ln -s /julia-${JULIA_VER}/bin/julia /usr/local/bin/julia
RUN mkdir /.julia && chown ${USER_ID} /.julia

RUN useradd --no-log-init --system --uid ${USER_ID} \
	--create-home --shell /bin/bash julia-user

USER ${USER_NAME}

# Package Installations

RUN julia -e 'Pkg.init()' && \
    julia -e 'Pkg.update()' && \
    julia -e 'Pkg.add("Yao")' && \
    julia -e 'Pkg.add("QuantumLab")' && \
    julia -e 'Pkg.add("QuantumInformation")' && \
    julia -e 'Pkg.add("QuantumOptics")' && \
    julia -e 'Pkg.add("Quante")' && \
    julia -e 'Pkg.add("Iterators")' && \
    julia -e 'Pkg.add("IJulia")' && \
    julia -e 'Pkg.add("Spectra")' && \
    julia -e 'Pkg.add("DataFrames")' && \
    julia -e 'Pkg.add("Flux")' && \
    julia -e 'Pkg.add("TensorFlow")' && \
    julia -e 'Pkg.add("Plots")' && \
    julia -e 'Pkg.add("PyCall")' && \
    julia -e 'Pkg.add("PyPlot")' && \
    julia -e 'Pkg.add("ExcelReaders")' && \
    julia -e 'Pkg.update()' && \
    julia -e 'Pkg.dev("https://github.com/QuantumBFS/QuAlgorithmZoo.jl.git")' && \
    julia -e 'using IJulia'