
General Approach

1. Started with an SConstruct file taken from (almost similar to) - [https://github.com/Juniper/contrail-build]().

2. Added following git submodules - (Local forks of original repos, so that I can push back changes).

 * https://github.com/hyphenOs/contrail-controller - controller (heads/devcontrail)
 * https://github.com/hyphenOs/contrail-generateDS - tools/generateds (heads/master)
 * https://github.com/hyphenOs/contrail-sandesh    - tools/sandesh (heads/master)
 * https://github.com/hyphenOs/contrail-vrouter    - vrouter (heads/master)

3. Updated dependencies.md as new packages are added - but this is likely not going to be complete as the system might already be in some state.

List of issues faced and changes done to original approach, while trying to build using `scons`.

1. Instead of following the complete `fetch_packages.py`, added a new tag `short_name` and we can download each package separately. This was done to avoid complete (and possibly redundant) download of the packages - This avoids downloading of certain packages -
  - icu4c (not used yet)
  - vijava (not used yet)

2. I believe Google Go is probably not needed as third party, `packages.xml` will have to be fixed accordingly.

3. Added two more (mainly because - something that is not available either as `official` package or `opencontrail:ppa` is `third_party` and should be treated as such. So we avoid doing `dpkg -i <package-name.deb> <xxxxx>`, either `apt-get` manages it or it's available as `third_party`.
  - librdkafka  (This is probably only Ubuntu 16.04 issue).
  - Cassandra CPP driver.

4. Changed the inside `controller/lib/SConscript` to add `libcql` and `librdkafka` as `subdirs`. (`libcql` was previously a dependency but probably got dropped due to `dpkg -i <cpp-driver.deb>`

5. Added following dependencies in `controlller/src/SConscript` (probably a side effect of 3. above)
  - Added `libuv`

6. Added following as a dependency in `controller/analytics/src`
  - Added `libdl` (Faced an error similar to [this](https://askubuntu.com/questions/334884/while-compiling-truecrypt-i-get-undefined-reference-to-symbol-dlcloseglibc)).

7. Fixed openvswitch `SConscript` to get `ln -sf` like beavior inside `controller/lib/openvswitch/SConscript`.


