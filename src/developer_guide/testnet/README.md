# rex-devnet

## Resources

[set up testnet](https://github.com/OLSF/libra/blob/d70716fb154339f4db71ae05edf8064013327b29/ol/documentation/core-devs/provision_dev_net.md)

## Quicksteps (verify) 
from @Daniyal

1. All the rex node runners need permission to write to the https://github.com/OLSF/dev-genesis repo (later a GitHub token needs to be generated and used on the node)

2. Cloning OLSF/libra , OLSF/dev-genesis and OLSF/dev-epoch-archive repos on the node.

3. installing all the dependencies (libra/util/setup.sh).

4. setting up a persona, there are 3 default personas, alice, bob, carol. For example the alice node environment needs to setup by running this command: export NODE_ENV=test NS=alice TEST=y. New nodes have to create a new layout (checkout the Genesis ceremony on the provision_dev_net.md doc)

5. running make dev-register only for the first time to setup the node.

6. running make devnet

## Volunteers Running Nodes 

Alice node, run by @daniyal: 148.251.89.142  
Bob node, run by @thenateway: 137.184.191.201  
Carol node, run by @o0l0o: 91.229.245.110  