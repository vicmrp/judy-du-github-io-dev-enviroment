# Use an official Python runtime as a parent image
# Use the official Node.js 20 image from Docker Hub
FROM node:20

# Set the working directory in the container
WORKDIR /usr/src/project




ARG DOCKERUSER_UID=65000
ARG DOCKERUSER_GID=65000
ARG DOCKERUSER_NAME=dockeruser
ARG DOCKERUSER_PASSWORD=dockeruser

ENV DOCKERUSER_UID=${DOCKERUSER_UID}
ENV DOCKERUSER_GID=${DOCKERUSER_GID}
ENV DOCKERUSER_NAME=${DOCKERUSER_NAME}
ENV DOCKERUSER_PASSWORD=${DOCKERUSER_PASSWORD}

###### fix locales ######
# Install locales package
RUN apt-get update && \
    apt-get install -y locales

# Generate the en_US.UTF-8 locale
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LC_ALL=en_US.UTF-8

# Set environment variables for locale
ENV LC_ALL=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
###### fix locales ######

# install basic utils
RUN apt-get update && apt-get install -y iputils-ping tree bash sudo gosu && rm -rf /var/lib/apt/lists/*

# Copy entrypoint script
COPY entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh



# Set entrypoint
ENTRYPOINT ["/entrypoint.sh"]

# Run app.py when the container launches
CMD ["/bin/bash"]
