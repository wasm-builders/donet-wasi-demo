FROM gitpod/workspace-dotnet

RUN sudo apt-get update && \
    sudo apt-get install gettext libncurses5 libxkbcommon0 libtinfo5 -y

USER gitpod

# subo 0.5.2
RUN brew tap suborbital/subo && \
    brew install subo

# ------------------------------------
# Install Sat (Suborbital)
# ------------------------------------
# "sat_version":"v0.1.4"
RUN git clone --depth=1 https://github.com/suborbital/sat.git && \
    cd sat && \
    go build -o .bin/sat -tags netgo,wasmtime . && \
    sudo cp .bin/sat /usr/local/bin/sat && \
    cd .. && \
    rm -rf sat

# ------------------------------------
# Install Wagi (Deislab)
# ------------------------------------
RUN mkdir tmp-wagi && \
    cd tmp-wagi && \
    wget https://github.com/deislabs/wagi/releases/download/v0.8.1/wagi-v0.8.1-linux-amd64.tar.gz && \
    tar -zxf wagi-v0.8.1-linux-amd64.tar.gz && \
    sudo cp wagi /usr/local/bin/wagi && \
    cd .. && \
    rm -rf tmp-wagi

# ------------------------------------
# Install Dot.NEt Core Preview
# ------------------------------------
#RUN wget https://download.visualstudio.microsoft.com/download/pr/322dd9d6-3135-4f8f-aa00-4daf61bc51d0/a4e28f08a42034b276e4536acdd0d7f0/dotnet-sdk-7.0.100-preview.4.22252.9-linux-x64.tar.gz

#RUN mkdir -p $HOME/dotnet && tar zxf dotnet-sdk-7.0.100-preview.4.22252.9-linux-x64.tar.gz -C $HOME/dotnet
#RUN rm dotnet-sdk-7.0.100-preview.4.22252.9-linux-x64.tar.gz

# ------------------------------------
# Install Wasi Runtimes
# ------------------------------------
RUN curl -sSf https://raw.githubusercontent.com/WasmEdge/WasmEdge/master/utils/install.sh | bash -s -- -v 0.10.0 && \
    curl https://get.wasmer.io -sSfL | sh && \
    curl https://wasmtime.dev/install.sh -sSf | bash

