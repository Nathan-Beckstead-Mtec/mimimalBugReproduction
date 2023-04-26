# Parser doesn't throw an error when a data bind only contains a comment
a bug I found in angular by Nathan Beckstead

### Description:

A data bind in the form of `{{//comment}}` in a component HTML file causes the compiler to freak out because something is undefined. I assume this should be handled in the same way `{{}}` is by throwing a Parser Error.


------------



**Similar data binds that correctly produce a Parser Error and their corresponding errors:**
- `{{}}`
	- `Error: src/app/app.component.html:16:1 - error NG5002: Parser Error: Blank expressions are not allowed in interpolated strings`
- `{{/*hello*/}}`
	- `Error: src/app/app.component.html:9:1 - error NG5002: Parser Error: Unexpected token /`
- `{{#!/usr/bin/env node}}`
	- `Error: src/app/app.component.html:11:1 - error NG5002: Parser Error: Lexer Error: Invalid character [#]`
	- `Error: src/app/app.component.html:11:1 - error NG5002: Parser Error: Unexpected token Lexer Error: Invalid character [#]`


### Environment:

```
Angular CLI: 15.2.7
Node: 16.20.0
Package Manager: npm 8.19.4
OS: linux x64

Angular: 15.2.8
... animations, common, compiler, compiler-cli, core, forms
... platform-browser, platform-browser-dynamic, router

Package                         Version
---------------------------------------------------------
@angular-devkit/architect       0.1502.7
@angular-devkit/build-angular   15.2.7
@angular-devkit/core            15.2.7
@angular-devkit/schematics      15.2.7
@angular/cli                    15.2.7
@schematics/angular             15.2.7
rxjs                            7.8.0
typescript                      4.9.5

```



### Error itself:
```
<e> [webpack-dev-middleware] TypeError: Cannot read properties of undefined (reading 'visit')
<e>     at _AstToIrVisitor._visit (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:7006:48)
<e>     at _AstToIrVisitor.visitInterpolation (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:6850:28)
<e>     at convertUpdateArguments (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:6669:32)
<e>     at TemplateDefinitionBuilder.getUpdateInstructionArguments (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:17846:33)
<e>     at Object.paramsOrFn (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:17667:125)
<e>     at getInstructionStatements (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:4858:90)
<e>     at TemplateDefinitionBuilder.buildTemplateFunction (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:17094:34)
<e>     at compileComponentFromMetadata (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler/fesm2015/compiler.mjs:18752:56)
<e>     at ComponentDecoratorHandler.compileFull (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:6529:17)
<e>     at TraitCompiler.compile (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:3742:36)
<e>     at IvyCompilationVisitor.visitClassDeclaration (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4070:37)
<e>     at file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4017:68
<e>     at IvyCompilationVisitor._visitListEntryNode (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4001:20)
<e>     at IvyCompilationVisitor._visit (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4017:26)
<e>     at file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4015:54
<e>     at visitArrayWorker (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:91402:48)
<e>     at visitNodes (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:91366:23)
<e>     at visitLexicalEnvironment (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:91432:22)
<e>     at visitEachChildOfSourceFile (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:91975:59)
<e>     at Object.visitEachChild (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:91546:42)
<e>     at IvyCompilationVisitor._visit (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4015:17)
<e>     at visit (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:3993:18)
<e>     at transformIvySourceFile (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4182:3)
<e>     at file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4058:52
<e>     at DelegatingPerfRecorder.inPhase (file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-YZWN2KWE.js:180:14)
<e>     at file:///home/user/minimalBugReproduction/node_modules/@angular/compiler-cli/bundles/chunk-KV5PW2QN.js:4058:19
<e>     at transformSourceFileOrBundle (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:92667:68)
<e>     at transformation (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112235:24)
<e>     at transformRoot (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112262:82)
<e>     at Object.transformNodes (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112246:78)
<e>     at emitJsFileOrBundle (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112913:32)
<e>     at emitSourceFileOrBundle (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112858:13)
<e>     at forEachEmittedFile (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112599:34)
<e>     at Object.emitFiles (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:112839:9)
<e>     at emitWorker (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:120249:33)
<e>     at /home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:120226:72
<e>     at runWithCancellationToken (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:120321:24)
<e>     at Object.emit (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:120226:26)
<e>     at Object.emit (/home/user/minimalBugReproduction/node_modules/typescript/lib/typescript.js:123733:57)
<e>     at Object.emitter (/home/user/minimalBugReproduction/node_modules/@ngtools/webpack/src/ivy/plugin.js:509:21)
<e>     at analyzingFileEmitter (/home/user/minimalBugReproduction/node_modules/@ngtools/webpack/src/ivy/plugin.js:464:29)
<e>     at async AngularWebpackPlugin.rebuildRequiredFiles (/home/user/minimalBugReproduction/node_modules/@ngtools/webpack/src/ivy/plugin.js:288:36)
<e>     at async /home/user/minimalBugReproduction/node_modules/@ngtools/webpack/src/ivy/plugin.js:230:13
```