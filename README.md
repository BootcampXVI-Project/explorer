## Configure

* Copy entire crypto artifact directory (organizations/) from your fabric network (e.g /fabric-samples/test-network)

    ```bash
    cp -r ../fabric-samples/SupplychainNetwork/organizations/ .
    ```

* Now, you should have the following files and directory structure.

    ```
    docker-compose.yaml
    config.json
    connection-profile/test-network.json
    organizations/ordererOrganizations/
    organizations/peerOrganizations/
    ...
    ```

    An alternative option is to export environment variables in your shell.

    ```bash
    export EXPLORER_CONFIG_FILE_PATH=./config.json
    export EXPLORER_PROFILE_DIR_PATH=./connection-profile
    export FABRIC_CRYPTO_PATH=./organizations
    ```

* Replace the user's certificate with an admin certificate and a secret (private) key in the connection profile (test-network.json). You need to specify the absolute path on the Explorer container.

    Before:
    ```json
    "SupplierMSP": {
			"mspid": "SupplierMSP",
			"adminPrivateKey": {
				"path": "/tmp/crypto/peerOrganizations/supplier.supplychain.com/users/Admin@supplier.supplychain.com/msp/keystore/2857c2d8f5cb8c7d5e09806fb40fd75cdbddba92683a862cef1f6fc0ef369594_sk"
			},
			"peers": ["peer0.supplier.supplychain.com"],
			"signedCert": {
				"path": "/tmp/crypto/peerOrganizations/supplier.supplychain.com/users/Admin@supplier.supplychain.com/msp/signcerts/cert.pem"
			}
		}
    ```

    After:
    ```json
    "SupplierMSP": {
			"mspid": "SupplierMSP",
			"adminPrivateKey": {
				"path": "/tmp/crypto/peerOrganizations/supplier.supplychain.com/users/Admin@supplier.supplychain.com/msp/keystore/?????????????????????_sk"
			},
			"peers": ["peer0.supplier.supplychain.com"],
			"signedCert": {
				"path": "/tmp/crypto/peerOrganizations/supplier.supplychain.com/users/Admin@supplier.supplychain.com/msp/signcerts/????????????????????cert.pem"
			}
		}
    ```
    **Make sure you replace all paths.**

## Start container services

* Run the following to start up explore and explorer-db services after starting your fabric network:

    ```shell
    $ docker-compose up -d
    ```
# Login with admin:adminpw

## Clean up

* To stop services without removing persistent data, run the following:

    ```shell
    $ docker-compose down
    ```

* In the docker-compose.yaml, two named volumes are allocated for persistent data (for Postgres data and user wallet). If you would like to clear these named volumes up, run the following:

    ```shell
    $ docker-compose down -v
    ```


