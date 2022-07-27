# issues

## Bugs

## CodeSmell

- **Make 'フィールド名' 'readonly'.**

  コンストラクターでのみ値の設定がされているフィールドには readonly をつける。

  > readonly fields can only be assigned in a class constructor. If a class has a field that’s not marked readonly but is only set in the constructor, it could cause confusion about the field’s intended use. To avoid confusion, such fields should be marked readonly to make their intended use explicit, and to prevent future maintainers from inadvertently changing their use.

- **The parameter name 'パラメータ名' is not declared in the argument list.**

  引数系の例外(ArgumentNullException)等を throw する場合は、パラメータに設定する値は引数の値とする。

  > Some constructors of the ArgumentException, ArgumentNullException
  > ArgumentOutOfRangeException and DuplicateWaitObjectException classes must be fed with a valid parameter name. This rule raises an issue in two cases:
  >
  > - When this parameter name doesn’t match any existing ones.
  > - When a call is made to the default (parameterless) constructor.

- **Rename parameter 'パラメータ名' to '既定クラスのパラメータ名' to match the base class declaration.**

  オーバーライドメソッドのパラメータ名は規定クラスのものと統一する。

  > The name of a parameter in an externally visible. This rule raises an issue when method override does not match the name of the parameter in the base declaration of the method, or the name of the parameter in the interface declaration of the method or the name of any other partial definition.

- **The logging message template should not vary between calls to 'LoggerExtensions.LogInformation(ILogger, string?, params object?[])'**

  Logging メッセージに動的な値が値が設定された時に発生する警告。
  現状テンプレート文字列等も警告の対象となるため、基本は無視で良い。
  今後のアップデートで警告対象が修正される可能性が高い。

  > The logging message template should not vary between calls.

- **Complete the task associated to this 'TODO' comment.**

  残っている Todo コメントを削除する。

  > TODO tags are commonly used to mark places where some more code is required, but which the developer wants to implement later.
  >
  > Sometimes the developer will not have the time or will simply forget to get back to that tag.
  >
  > This rule is meant to track those tags and to ensure that they do not go unnoticed.

- **Remove this commented out code.**

  コメントアウトされているソースを削除する。

  > Programmers should not comment out code as it bloats programs and reduces readability.
  >
  > Unused code should be deleted and can be retrieved from source control history if required.

- **Remove this unread private field 'ErrorMessage' or refactor the code to use its value.**

  使用していいない private フィールドを削除する。

  > Private fields only used to store values without reading them later is a case of dead store. So changing the value of such field is useless and most probably indicates a serious error in the code.

- **Rename this enumeration to remove the 'Enum' suffix.**

  Enum の名称に接尾辞として"Enum"を付けている場合は、削除する。
  列挙型であることは型情報で認識できるため名称には含めない。

  > The information that an enumeration type is actually an enumeration or a set of flags should not be duplicated in its name.

- **Cognitive Complexity of methods should not be too high**

  可読性の低いコードのリファクトを行う。
  Where 等のパラメータの条件判定関数内で三項演算子や if を使用指定いる場合、パイプを使用するなど。

  > Cognitive Complexity is a measure of how hard the control flow of a method is to understand. Methods with high Cognitive Complexity will be difficult to maintain.

- **Extract this nested ternary operation into an independent statement.**

  ネストのある三項演算子を修正する。if で表現するなどネストされた三項演算子を分解する。

  > Just because you can do something, doesn’t mean you should, and that’s the case with nested ternary operations. Nesting ternary operators results in the kind of code that may seem clear as day when you write it, but six months later will leave maintainers (or worse - future you) scratching their heads and cursing.
  >
  > Instead, err on the side of clarity, and use another line to express the nested operation as a separate statement.

-
