# https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#create-and-build-the-dockerfile-1

ARG TARGETARCH=linux-arm
FROM ubuntu:18.04

ENV DEBIAN_FRONTEND=noninteractive
# RUN echo "APT::GEt::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

RUN apt-get update && apt-get install -y --no-install-recommends \
		ca-certificates \
		curl \
		jq \
		git \
		iputils-ping \
		libcurl4 \
		libicu60 \
		libunwind8 \
		netcat \
		libssl1.0 \
	&& rm -Rf /var/lib/apt/lists/*

RUN curl -LsS "https://aka.ms/InstallAzureCLIDeb" | bash \
	&& rm -Rf /var/lib/apt/lists/*

# Can be 'linux-x64', 'linux-arm64', 'linux-arm', 'rhel.6-x64'
ENV TARGETARCH=linux-arm

WORKDIR /azp

COPY ./start.bash .
RUN chmod +x start.bash && chown 1000:1000 /azp
USER 1000:1000

ENTRYPOINT ["./start.bash"]
