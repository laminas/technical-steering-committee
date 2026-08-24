# Next Technical Steering Committee Meeting Agenda

- Date: 2026-08-03
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

### Consider StructArmed for Architecture Guarding

I built [StructArmed](https://github.com/boundwize/structarmed), a PHP architecture guard that turns architectural decisions into executable checks.

It is already used by several PHP frameworks:

| Project          | Configuration                                                                                |
| ---------------- | -------------------------------------------------------------------------------------------- |
| CakePHP          | https://github.com/cakephp/cakephp/blob/5.x/structarmed.php               |
| CodeIgniter 4    | https://github.com/codeigniter4/CodeIgniter4/blob/develop/structarmed.php |
| Spiral Framework | https://github.com/spiral/framework/blob/master/structarmed.php           |

I would like us to consider whether StructArmed could also be useful for Laminas and Mezzio.

As a starting point, I suggest trying it on a small number of core packages:

* `mezzio/mezzio`
* `laminas/laminas-diactoros`

or another packages if there are better candidate.

Deptrac already covers the core architecture-layer use case well. Comparing to deptrac, the following are capabilities or characteristics of StructArmed that may be useful for Laminas/Mezzio:

| Area                     | StructArmed                                                                                                                                                             |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Configuration            | Native PHP configuration                                                                                                                                                |
| Getting started          | Ready-made presets, such as PSR-4, with layers, layer patterns, and rulesets added gradually as needed                                                                  |
| Preset customization     | Registered preset rules can be overridden, replaced, or skipped                                                                                                         |
| PHPUnit integration      | Can run as a PHPUnit extension                                                                                                                                          |
| Platform support         | Tested on Windows, macOS, and Linux                                                                                                                                     |
| Performance              | Optimized parallel analysis with optional caching                                                                                                                       |
| Extensibility            | Supports custom rules and custom fixers                                                                                                                                 |
| Automatic fixes          | Custom rules can implement `FixableInterface` and support `--fix`                                                                                                       |
| Parser/fixer integration | Custom rules and fixers can use `php-parser`, [JsonRecast](https://github.com/boundwize/jsonrecast), or their own implementation                                        |
| Dependencies             | Small set of direct runtime dependencies: [composer.json](https://github.com/boundwize/structarmed/blob/927f8c16de216ea46089e75a8d47b7cce07ba3b3/composer.json#L31-L34) |
| Tests                    | 100% test coverage                                                                                                                                                      |

Here performance tested on `Spiral Framework` and `CodeIgniter 4`:

* **Spiral Framework:** 2,212 files analyzed in **5.52 seconds** on a 2-core GitHub Actions runner: [reference](https://github.com/spiral/framework/actions/runs/30997621072/job/92278432577#step:9:26)
* **CodeIgniter 4:** with the StructArmed cache restored, analysis completed in **0.07 seconds**: [reference](https://github.com/codeigniter4/CodeIgniter4/actions/runs/30652213832/job/91227964459#step:10:13)

Full documentation is available at:

https://boundwize.github.io/structarmed/
