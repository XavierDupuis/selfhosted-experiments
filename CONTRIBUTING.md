# Contributing Guide

Thank you for considering contributing to this repository! To maintain consistency and ensure a smooth experience for users, please follow the guidelines below when adding new Docker Compose files.

## Submitting a Contribution

1. Fork the repository and create a new branch for your contribution.
2. Ensure your Docker Compose file follows the standards outlined below.
3. Provide a clear and concise README in the subdirectory if additional instructions are needed.
4. Submit a pull request, including a brief description of your contribution.

> Thank you for contributing and helping maintain a high standard for this repository!

## Contribution Standards

### > Directory Structure

    - The directory structure should be as follows:
    ```bash
        example_service/
        ├── docker-compose.yml       
        ├── .env.template           
        ├── README.md                
        ├── other_configuration_file 
        └── ...
    ```

### > Launching
  - Ensure that the Docker Compose file works with the command `docker-compose up -d`. 
  - If a different command is required, clearly document it in the README within the subdirectory.

### > Configuration

 - **Environment Variables:**

    - Ensure to include a meaningful `.env.template` file that serves as a template for users to configure their environment variables.
    - Clearly document all required variables and their default values in the `.env.template` file. 
        - Users should copy this template to create their `.env` file with personalized values.

    ```bash
        # .env.template

        # Base directory variable for local mapping
        DIRECTORY=/path/to/base/directory

        # Service version
        VERSION=latest

        # Service-specific environment variables with default values
        SOMEVAR=default_value
        ANOTHERVAR=another_default_value

        # Port configuration with default value
        SERVICE_PORT=8080

        # API Key for the service
        SERVICE_API_KEY=your_api_key

        # Database password
        DATABASE_PASSWORD=your_database_password

    ```

 - **Additional Configuration Files:**

   - If additional configuration files are needed for the service, include them in the directory.
   - Document how these configuration files should be used in the service-specific README.

### > Docker compose file

 - **Service Version:**

   - Include the service version in both the Docker Compose file and the .env.template file.
     ```yaml
     services:
       example_service:
         image: example-image:${SERVICE_VERSION:-latest}
     ```

 - **Environment Variables:**
   
   - Use the following syntax for required environment variables in the Docker Compose file:
     ```yaml
     services:
       example_service:
         environment:
           - "${SOMEVAR:?Missing variable SOMEVAR}"
     ```
   - Provide default version `latest`
   - [Learn more about Docker environment variables](https://docs.docker.com/compose/environment-variables/).

 - **Volumes and Local Mappings:**

   - Specify volumes and local mappings on the host machine using environment variables in `.env.template`.
     ```yaml
     services:
       example_service:
         volumes:
           - "${DIRECTORY:?Missing variable DIRECTORY}/example_service/data:/data"
     ```
   - Specify volumes as "read-only" when the service doesn't need to edit data.
   - [Learn more about Docker volumes and bind mounts](https://docs.docker.com/storage/volumes/).

 - **Port Mapping:**

   - Clearly specify opened ports with variable names in the corresponding `.env.template`.
     ```yaml
     services:
       example_service:
         ports:
           - "${SERVICE_PORT:-80}:80"
     ```
   - Provide default ports values
   - [Learn more about Docker port mapping](https://docs.docker.com/compose/compose-file/compose-file-v3/#ports).

 - **Restart Policy:**

   - Specify a restart policy for each container, with "unless-stopped" as the default choice. 
   - Include comments to motivate other options if necessary. 
   - [Learn more about Docker restart policies](https://docs.docker.com/config/containers/start-containers-automatically/#restart-policy).

 - **Container Naming:** 

    - Provide a meaningful `container_name` for every container.


