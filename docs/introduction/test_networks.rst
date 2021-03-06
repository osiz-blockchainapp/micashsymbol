.. _test-networks:

Test Networks
=============

Mainnet is the main Tezos network, but is not appropriate for testing.
Other networks are available to this end. Test networks usually run
with different constants to speed up the chain.

All networks share the same faucet: https://faucet.tzalpha.net/.
The keys obtained from this faucet can be used in all test networks.

Zeronet
-------

- Git branch: ``zeronet``
- Run Docker image: ``wget -O zeronet.sh https://gitlab.com/tezos/tezos/raw/zeronet/scripts/alphanet.sh``

Zeronet is an unstable test network.
It is often reset to keep the chain short and to allow testing of
protocols which are being developed.

On Zeronet, the following constants differ from Mainnet:

- ``blocks_per_cycle`` is 128 instead of 4096;
- ``blocks_per_roll_snapshot`` is 8 instead of 256;
- ``blocks_per_voting_period`` is 2816 instead of 32768;
- ``time_between_blocks`` is ``[ 20 ]`` instead of ``[ 60, 40 ]``;
- ``test_chain_duration`` is 43200 instead of 1966080;
- ``quorum_min`` is 3000 (i.e. 30%) instead of 2000 (i.e. 20%);
- ``delay_per_missing_endorsement`` is 2 instead of 8.

This results in a chain which moves faster:

- 3 blocks per minute instead of 1,
- one cycle should last less than 43 minutes instead of 2 days and 20 hours,
- a voting period should last less than 16 hours instead of about 23 days.
Note that in Zeronet, a voting period is 22 cycles instead of 8 cycles in Mainnet.

Carthagenet
-----------

- Git branch: ``carthagenet``
- Run Docker image: ``wget -O carthagenet.sh https://gitlab.com/tezos/tezos/raw/carthagenet/scripts/alphanet.sh``

Carthagenet is a test network which was started with the Babylon protocol,
and which will be upgraded with the Carthage protocol by vote once Carthage
is ready. If Carthage becomes the active protocol of Mainnet,
Carthagenet will run until Carthage is replaced by another protocol.
If Carthage is not activated on Mainnet, Carthagenet will also end.

On Carthagenet, the following constants differ from Mainnet:

- ``preserved_cycles`` is 3 instead of 5;
- ``blocks_per_cycle`` is 2048 instead of 4096;
- ``blocks_per_voting_period`` is 2048 instead of 32768;
- ``time_between_blocks`` is ``[ 30, 40 ]`` instead of ``[ 60, 40 ]``;
- ``test_chain_duration`` is 43200 instead of 1966080;
- ``quorum_min`` is 3000 (i.e. 30%) instead of 2000 (i.e. 20%);

This results in a faster chain than Mainnet, but not quite as fast as Zeronet:

- 2 blocks per minute;
- a cycle should last about 17 hours;
- a voting period lasts 1 cycle and should thus also last about 17 hours.

Babylonnet
----------

- Git branch: ``babylonnet``
- Run Docker image: ``wget -O babylonnet.sh https://gitlab.com/tezos/tezos/raw/babylonnet/scripts/alphanet.sh``

Babylonnet is a test network which runs the Babylon protocol.
It was spawned after the injection of the proposal for Babylon.
It will run until Babylon is no longer the active protocol of Mainnet.

On Babylonnet, the following constants differ from Mainnet:

- ``preserved_cycles`` is 3 instead of 5;
- ``blocks_per_cycle`` is 2048 instead of 4096;
- ``blocks_per_voting_period`` is 8192 instead of 32768;
- ``time_between_blocks`` is ``[ 30, 40 ]`` instead of ``[ 60, 40 ]``;
- ``test_chain_duration`` is 86400 instead of 1966080;
- ``quorum_min`` is 3000 (i.e. 30%) instead of 2000 (i.e. 20%);
- ``delay_per_missing_endorsement`` is 2 instead of 8.

This results in a faster chain than Mainnet, but not quite as fast as Zeronet:

- 2 blocks per minute,
- a cycle should last about 17 hours,
- a voting period lasts 4 cycles and should be about 2 days and 20 hours.

Deposits are also smaller, which means that you do not need as many tez to
bake continuously.

Future Networks
---------------

At some point, there will be a proposal for a successor to the current
protocol (let's call this new protocol P). After P is injected, a new test network
(let's call it P-net) will be spawned. It will run alongside the latest
test network until either P is rejected or activated. If P is rejected, P-net will
end, unless P is immediately re-submitted for injection. If, however,
P is activated, the previous test network will end and P-net will continue on its own.

Old Networks
------------

Alphanet was the test network before Babylonnet. At the end of its life,
it was running the Athens protocol. Bootstrap nodes were shut down after
the Babylon protocol was activated on Mainnet.
