Step-by-step guide to installing Elasticsearch on macOS


1. Download Elasticsearch 8.12.2:

· Go to the Elasticsearch downloads page: [Elasticsearch Download](https://www.elastic.co/downloads/elasticsearch)

· Choose the appropriate package for macOS (usually the.tar.gz version).

· Once downloaded, extract the contents of the downloaded file to a directory of your choice.



2. Disable Security in elasticsearch.yml:

· Navigate to the Elasticsearch configuration directory. By default, it's located in config within the Elasticsearch directory.

· Open the elasticsearch.yml file using a text editor.

· Add the following line to the file to disable security:

            xpack.security.enabled: false

· Save and close the file.



3. Start Elasticsearch:

· Open Terminal on your macOS.

· Navigate to the directory where you extracted Elasticsearch in Step 1.

· Change directory to the bin folder within the Elasticsearch directory.

· Run the following command to start Elasticsearch:

               ./elasticsearch

· Elasticsearch will start running. Wait for a moment until you see log messages indicating that the server has started successfully.



4. Verify Elasticsearch Installation:

· Open a web browser.

· Go to http://localhost:9200/ in the address bar.

· You should see a JSON response indicating that Elasticsearch is up and running, along with version information.



-----------------------------------------------------------------------------------------------------------------------

Step-by-step guide to installing Elasticsearch on Linux


1. Download Elasticsearch 8.12.2:

· Visit the Elasticsearch downloads page: Elasticsearch Download

· Choose the appropriate package for Linux (usually the .tar.gz version).

· Once downloaded, extract the contents of the downloaded file to a directory of your choice.



2. Disable Security in elasticsearch.yml:

· Navigate to the Elasticsearch configuration directory. By default, it's located in config within the Elasticsearch directory.

· Open the elasticsearch.yml file using a text editor.

· Add the following line to the file to disable security:

             xpack.security.enabled: false

· Save and close the file.



3. Start Elasticsearch:

· Open Terminal on your Linux system.

· Navigate to the directory where you extracted Elasticsearch in Step 1.

· Change directory to the bin folder within the Elasticsearch directory.

· Run the following command to start Elasticsearch:

             ./elasticsearch

· Elasticsearch will start running. Wait for a moment until you see log messages indicating that the server has started successfully.



4. Verify Elasticsearch Installation:

· Open a web browser.

· Go to http://localhost:9200/ in the address bar.

· You should see a JSON response indicating that Elasticsearch is up and running, along with version information.