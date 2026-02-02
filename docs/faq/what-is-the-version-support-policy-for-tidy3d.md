# What is the version support policy for Tidy3D?

| Date       | Category    |
|------------|-------------|
| 2026-02-02 12:00:00 | Installation and Help |


Tidy3D follows <a target="_blank" rel="noopener" href="https://semver.org/">semantic versioning</a>. This means:

<ul>
<li><strong>Patch versions</strong> (<code>x.y.*</code>): Components are fully backwards- and forwards-compatible within the same minor version.</li>
<li><strong>Minor versions</strong> (<code>x.*</code>): Components are backwards-compatible within the same major version. For example, version <code>x.y1.z1</code> can always load components created with <code>x.y2.z2</code> if <code>y1 >= y2</code>.</li>
</ul>

<strong>Important exceptions:</strong>

<ul>
<li><strong>Plugins</strong> may introduce breaking changes between versions and do not strictly follow the compatibility rules above.</li>
<li>In rare cases, there may be small breaking changes to core components, typically for features introduced recently. Similarly, there could be changes that do not affect component schemas but affect solver results (e.g., due to interpretation of some parameters). We always minimize these, and they are documented in a dedicated section in the <a target="_blank" rel="noopener" href="https://docs.flexcompute.com/projects/tidy3d/en/stable/changelog.html">changelog</a>.</li>
</ul>

<strong>Support lifecycle:</strong>

<ul>
<li>Each minor version is supported for approximately one year after the release of its last patch.</li>
<li>After support is dropped, submitting a task to the server will return an error prompting you to upgrade.</li>
<li>Simulations and data created with older versions can still be loaded after upgrading, due to the backwards compatibility guarantees described above.</li>
<li>The web GUI always uses the latest stable minor version.</li>
</ul>

<strong>Pre-release versions:</strong>

Release candidate (<code>rc</code>) and development (<code>dev</code>) versions are temporary and can be used to explore new features. However:

<ul>
<li>Compatibility of newly introduced features is not guaranteed—they may change before the official release.</li>
<li>Support for pre-release versions may be dropped shortly after the corresponding stable release is available.</li>
<li>You should upgrade to the stable release as soon as it becomes available.</li>
</ul>
