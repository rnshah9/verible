---
---

# `verilog_lint`

Tool for formatting Verilog and SystemVerilog code. Part of the verible tool
suite.

## Command line arguments

```
verilog_lint: usage: bazel-bin/verilog/tools/lint/verilog_lint [options] <file> [<file>...]

  Flags from external/com_google_absl/absl/flags/parse.cc:
    --flagfile (comma-separated list of files to load flags from); default: ;
    --fromenv (comma-separated list of flags to set from the environment [use
      'export FLAGS_flag1=value']); default: ;
    --tryfromenv (comma-separated list of flags to try to set from the
      environment if present); default: ;
    --undefok (comma-separated list of flag names that it is okay to specify on
      the command line even if the program does not define a flag with that
      name); default: ;


  Flags from external/com_google_absl/absl/flags/internal/usage.cc:
    --help (show help on important flags for this binary [tip: all flags can
      have two dashes]); default: false;
    --helpfull (show help on all flags); default: false; currently: true;
    --helpmatch (show help on modules whose name contains the specified substr);
      default: "";
    --helpon (show help on the modules named by this flag value); default: "";
    --helppackage (show help on all modules in the main package);
      default: false;
    --helpshort (show help on only the main module for this program);
      default: false;
    --only_check_args (exit after checking all flags); default: false;
    --version (show version and build info and exit); default: false;


  Flags from verilog/analysis/verilog_linter.cc:
    --rules (Comma-separated of lint rules to enable. No prefix or a '+' prefix
      enables it, '-' disable it. Configuration values for each rules placed
      after '=' character.); default: ;
    --rules_config (Path to lint rules configuration file. Disables
      --rule_config_search.); default: ".rules.verible_lint";
    --rules_config_search (Look for lint rules configuration file, searching
      upward from the location of each analyzed file.); default: false;
    --ruleset ([default|all|none], the base set of rules used by linter);
      default: default;
    --waivers_file (Path to waivers file. Please refer to the README file for
      information about its format.); default: "";


  Flags from verilog/parser/verilog_parser.cc:
    --verilog_trace_parser (Trace verilog parser); default: false;


  Flags from verilog/tools/lint/verilog_lint.cc:
    --generate_markdown (If true, print the description of every rule formatted
      for the markdown and exit immediately. Intended for the output to be
      written to a snippet of markdown.); default: false;
    --help_rules ([all|<rule-name>], print the description of one rule/all rules
      and exit immediately.); default: "";
    --lint_fatal (If true, exit nonzero if linter finds violations.);
      default: false;
    --parse_fatal (If true, exit nonzero if there are any syntax errors.);
      default: false;
```

## Lint Rules

### always-comb
Checks that there are no occurrences of `always @*`. Use `always_comb` instead. See [Style: combinational-logic].

Enabled by default: true

### always-comb-blocking
Checks that there are no occurrences of non-blocking assignment in combinational logic.

Enabled by default: true

### always-ff-non-blocking
Checks that there are no occurrences of blocking assignment in sequential logic.

Enabled by default: true

### case-missing-default
Checks that a default case-item is always defined. See [Style: case-statements].

Enabled by default: true

### constraint-name-style
Check that constraint names follow the lower_snake_case convention and end with _c. See [Style: constraints].

Enabled by default: false

### create-object-name-match
Checks that the 'name' argument of `type_id::create()` matches the name of the variable to which it is assigned. See [Verification-Style: naming].

Enabled by default: true

### endif-comment
Checks that a Verilog `` `endif`` directive is followed by a comment that matches the name of the opening `` `ifdef`` or `` `ifndef``. See [Style: endif-comment].

Enabled by default: false

### enum-name-style
Checks that `enum` names use lower_snake_case naming convention and end with '_t' or '_e'. See [Style: enumerations].

Enabled by default: true

### explicit-function-lifetime
Checks that every function declared outside of a class is declared with an explicit lifetime (static or automatic). See [Style: function-task-explicit-lifetime].

Enabled by default: true

### explicit-function-task-parameter-type
Checks that every function and task parameter is declared with an explicit storage type. See [Style: function-task-argument-types].

Enabled by default: true

### explicit-parameter-storage-type
Checks that every `parameter` and `localparam` is declared with an explicit storage type. See [Style: constants].
##### Parameters
  * `exempt_type` (optional `string`. Default: empty)

Enabled by default: true

### explicit-task-lifetime
Checks that every task declared outside of a class is declared with an explicit lifetime (static or automatic). See [Style: function-task-explicit-lifetime].

Enabled by default: true

### forbid-consecutive-null-statements
Checks that there are no occurrences of consecutive null statements like `;;`

Enabled by default: true

### forbid-defparam
Do not use defparam. See:[Style: defparam].

Enabled by default: true

### forbidden-macro
Checks that no forbidden macro calls are used. See [Verification-Style: logging].

Enabled by default: true

### generate-label
Checks that every generate block statement is labeled. See [Style: generate-statements].

Enabled by default: true

### interface-name-style
Checks that `interface` names use lower_snake_case naming convention and end with '_if'. See [Style: interface-conventions].

Enabled by default: true

### invalid-system-task-function
Checks that no forbidden system tasks or functions are used. These consist of the following functions: `$psprintf`, `$random`, and `$dist_*`. Also non-LRM function `$srandom`. See [Verification-Style: forbidden-system-functions].

Enabled by default: true

### line-length
Checks that all lines do not exceed the maximum allowed length. See [Style: line-length].
##### Parameters
  * `length` Default: `100`

Enabled by default: true

### macro-name-style
Checks that every macro name follows ALL_CAPS naming convention. See [Style: defines].

Enabled by default: true

### mismatched-labels
Labels mismatch. See:[Style: mismatched-labels].

Enabled by default: false

### module-begin-block
Checks that there are no begin-end blocks declared at the module level. See [Style: floating-begin-end-blocks].

Enabled by default: true

### module-filename
If a module is declared, checks that at least one module matches the first dot-delimited component of the file name.  See [Style: file-names].

Enabled by default: true

### module-parameter
Checks that module instantiations with more than one parameter are passed in as named parameters, rather than positional parameters. See [Style: module-instantiation].

Enabled by default: true

### module-port
Checks that module instantiations with more than one port are passed in as named ports, rather than positional ports. See [Style: module-instantiation].

Enabled by default: true

### no-tabs
Checks that no tabs are used. Spaces should be used instead of tabs. See [Style: tabs].

Enabled by default: true

### no-trailing-spaces
Checks that there are no trailing spaces on any lines. See [Style: trailing-spaces].

Enabled by default: true

### one-module-per-file
Checks that at most one module is declared per file. See [Style: file-extensions].

Enabled by default: false

### package-filename
Checks that the package name matches the filename. See [Style: file-names].

Enabled by default: true

### packed-dimensions-range-ordering
Checks that packed dimension ranges are declare in little-endian (decreasing) order, e.g. `[N-1:0]`. See [Style: packed-ordering].

Enabled by default: true

### parameter-name-style
Checks that non-type parameter and localparam names follow at least one of the naming conventions from a choice of CamelCase and ALL_CAPS, ORed together with the pipe-symbol(|). Empty configuration: no style enforcement. See [Style: constants].
##### Parameters
 * `localparam_style` Default: `CamelCase`
 * `parameter_style` Default: `CamelCase|ALL_CAPS`


Enabled by default: true

### parameter-type-name-style
Checks that parameter type names follow the lower_snake_case naming convention and end with _t. See [Style: parametrized-objects].

Enabled by default: false

### plusarg-assignment
Checks that plusargs are always assigned a value, by ensuring that plusargs are never accessed using the `$test$plusargs` system task. See [Style: plusarg-value-assignment].

Enabled by default: true

### positive-meaning-parameter-name
Checks that no parameter name starts with 'disable', using positive naming (starting with 'enable') is recommended. See [Style: binary-parameters].

Enabled by default: true

### posix-eof
Checks that the file ends with a newline. See [Style: posix-file-endings].

Enabled by default: true

### proper-parameter-declaration
Checks that every `parameter` declaration is inside a package or in the formal parameter list of modules/classes and every `localparam` declaration is inside a module or class. See [Style: constants].

Enabled by default: false

### signal-name-style
Checks that signal names use lower_snake_case naming convention. Signals are defined as "a net, variable, or port within a SystemVerilog design".  See [Style: signal-conventions].

Enabled by default: false

### struct-union-name-style
Checks that `struct` and `union` names use lower_snake_case naming convention and end with '_t'. See [Style: struct-union-conventions].

Enabled by default: true

### typedef-enums
Checks that a Verilog `enum` declaration is named using `typedef`. See [Style: typedef-enums].

Enabled by default: true

### typedef-structs-unions
Checks that a Verilog `struct` or `union` declaration is named using `typedef`. See [Style: typedef-structs-unions].
##### Parameters
  * `allow_anonymous_nested` Default: `false`

Enabled by default: true

### undersized-binary-literal
Checks that the digits of binary literals match their declared width. See [Style: number-literals].

Enabled by default: true

### unpacked-dimensions-range-ordering
Checks that unpacked dimension ranges are declared in big-endian order, `[0:N-1]` and when an unpacked dimension range is zero-based, `[0:N-1]`, the size is declared as `[N]` instead. See [Style: unpacked-ordering].

Enabled by default: true

### v2001-generate-begin
Checks that there are no generate-begin blocks inside a generate region. See [Style: generate-constructs].

Enabled by default: true

### void-cast
Checks that void casts do not contain certain function/method calls. See [Verification-Style: void-casts].

Enabled by default: true


## Version

Generated on 2020-05-21 14:59:48 -0700 from [v0.0-407-g629d890](https://github.com/google/verible/commit/629d8908d05d895ca1586e98bd73284ad41b77f4)