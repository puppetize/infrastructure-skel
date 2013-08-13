= Daft Opinions


== Opinion 1: Executable scripts instead of Rake tasks and such

**Origin**: Inspired by GitHub, as are the names of the scripts used
in this repository.

**Pros**:
- One less tool to learn.
- Lower bar to add new tasks.

**Cons**:
- Calling conventions for different scripts could vary widely.
- No out-of-the-box way to generate a list of tasks with at least a
  short description (as in `rake -T`).


== Discussion: r10k vs. librarian-puppet vs. git submodules


=== Opinion 2.1: git alone is sufficient to manage Puppet modules

**Origin**: Personal opinion, grown out of a) frustration with the way
the specialized tools are distributed (RubyGems), so that they're not
available out of the box, and b) having to show novice users a lot of
tools that where, taken all together, overwhelming for many.

**Pros**:
- One less tool to learn.
- Many resources available on how to work with git submodules.

**Cons**:
- Only applicable where the choice of version control system is git.
- Requires slightly elevated git skills.
- Can be cumbersome when the implementation of a feature requires
  changes to modules and site-specific code.
- Certain modifications, like replacing a directory with a submodule,
  don't seem to go down well with `git submodule update`, at least not
  at the time of this writing.
- The implementation of submodules as of git 1.8 may still be changed
  and that could cause some disruption to Puppet users.  For example,
  submodules' .git directories have been replaced by a file that now
  contains an absolute path.  That seems to have been a rather recent
  change, and it means that repository trees can no longer be copied
  easily within the filesystem.  I don't think that this will be the
  final iteration of the git submodule design.


=== Opinion 2.2: Use "puppet module" tool for module management

**Origin**: Puppet's own [online documentation][1].

[1]: http://docs.puppetlabs.com/puppet/2.7/reference/modules_installing.html
     "Installing Modules -- Puppet 2.7 Documentation"

**Pros**:
- It's officially supported by Puppet Labs.
- Once installed, modules can be managed with any version control system.
- A Puppet infrastructure repository that includes all modules is fully
  self-contained and be used right away after checking out the work tree.

**Cons**:
- `puppet module` can only install modules that have been published on
  PuppetForge and does not support installation from the module "source"
  (e.g., repositories on GitHub or an internal repository manager).
