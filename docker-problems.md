### Error: failed to solve with frontend dockerfile.v0 
When: While trying to build the docker images 

Solution: `rm /Users/<username>/.docker/buildx/current`

---------------------------------------------------------------------------------------

### Error: dockerpycreds.errors.StoreError: Credentials store docker-credential-desktop exited with "error listing credentials - err: exit status 1, out: `The specified item could not be found in the keychain.`".
When: docker-compose

Solution: 
```
nano ~/.docker/config.json 
remove: "credsStore": desktop
```
