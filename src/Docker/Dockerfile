ARG REGISTRY='docker.io'
ARG DISTRO='alpine.3.14'
ARG DOTNET_VERSION='5.0'

FROM $REGISTRY/gittools/build-images:$DISTRO-sdk-$DOTNET_VERSION as build
ARG contentFolder

WORKDIR /root
RUN git clone -b feature/read-only-root https://github.com/taylorjonl/GitVersion.git \
    && dotnet publish -f "net5.0" -o /app ./GitVersion/src/GitVersion.App/GitVersion.App.csproj

FROM $REGISTRY/gittools/build-images:$DISTRO-runtime-$DOTNET_VERSION

WORKDIR /tools
COPY --from=build /app .

ENV COMPlus_EnableDiagnostics="0"

ENTRYPOINT ["/tools/gitversion"]
