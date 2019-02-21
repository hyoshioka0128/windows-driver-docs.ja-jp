---
title: フレームワークを確認します。
description: フレームワークを確認します。
ms.assetid: A954B5E2-E3C7-4021-BE53-AE1257139607
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a9aaf7a41b6a6d0f1c137c2c456cf0283d22a98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56537646"
---
# <a name="verify-framework"></a>フレームワークを確認します。


TAEF を簡単にテストを作成するには、利用する「確認」フレームワークを提供します、 [WexLogger](wexlogger.md)最小限のコードの詳細なログを報告します。 検証フレームワークにより、構造化ログ出力を提供するためのテスト - 特定の検証が成功し、検証に失敗した場合は、詳細な情報が出力に成功したログを出力します。

## <a name="span-idcplusplusspanspan-idcplusplusspanusing-verify-from-c"></a><span id="cplusplus"></span><span id="CPLUSPLUS"></span>C++ から使用して確認します


確認 API は、C++ では、一連の"Verify.h"ヘッダー ファイルで定義されているマクロとして表示されます (注。Verify.h を明示的に指定する必要はありません、マーキング アップ C++ のテストと検証および WexLogger の API と対話するのに必要なすべてを含む"WexTestClass.h"を含める必要があります)。

次のことを確認のマクロは、ネイティブの C++ テスト使用できます。

| マクロ                                                                                     | 機能                                                                                                                                                                                                         |
|-------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 確認\_は\_と等しい (予想される、実際、\[省略可能なメッセージ\])                                | 2 つの指定したオブジェクトが等しいことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                                |
| 確認してください\_は\_いない\_等しい (予想される、実際、\[省略可能なメッセージ\])                           | 2 つの指定したオブジェクトが等しくないことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                            |
| 確認\_IS\_GREATER\_より (expectedGreater、expectedLess、\[省略可能なメッセージ\])            | 最初のパラメーターが 2 番目のパラメーターより大きいことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                       |
| 確認\_IS\_GREATER\_より\_または\_等しい (expectedGreater、expectedLess、\[省略可能なメッセージ\]) | 最初のパラメーターが 2 番目のパラメーター以上であることを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                           |
| 確認\_IS\_少ない\_より (expectedLess、expectedGreater、\[省略可能なメッセージ\])               | 最初のパラメーターが小さいことを確認します。 2 番目のパラメーターよりもします。 指定されている場合は、カスタム メッセージを記録します。                                                                                                          |
| 確認\_IS\_少ない\_より\_または\_と等しい (expectedLess、expectedGreater、\[省略可能なメッセージ\])    | 最初のパラメーターが 2 番目のパラメーター以下であることを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                              |
| 確認\_は\_同じ (予想される、実際、\[省略可能なメッセージ\])                                 | 指定された 2 つのパラメーターが同じオブジェクトを参照していることを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                          |
| 確認してください\_は\_いない\_同じ (予想される、実際、\[省略可能なメッセージ\])                            | 指定された 2 つのパラメーターが同じオブジェクトを参照しないことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                   |
| 確認\_失敗 (\[省略可能なメッセージ\])                                                       | 条件を確認しないで失敗します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                                        |
| 確認\_IS\_TRUE (条件、\[省略可能なメッセージ\])                                         | 指定したブール値が true であることを確認します。 検証を呼び出す\_IS\_TRUE (!!\_\_条件)、または確認\_WIN32\_BOOL\_SUCCEEDED (\_\_条件) Win32 bool 型の値をテストします。 指定されている場合は、カスタム メッセージを記録します。                      |
| 確認\_IS\_FALSE (条件、\[省略可能なメッセージ\])                                        | 指定したブール値が false であることを確認します。 検証を呼び出す\_IS\_FALSE (!!\_\_条件)、または確認\_WIN32\_BOOL\_FAILED (\_\_条件) Win32 bool 型の値をテストします。 指定されている場合は、カスタム メッセージを記録します。                       |
| 確認\_IS\_NULL (オブジェクト、\[省略可能なメッセージ\])                                            | 指定されたパラメーターが NULL であることを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                                |
| 確認\_IS\_いない\_NULL (オブジェクト、\[省略可能なメッセージ\])                                       | 指定されたパラメーターが NULL でないことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                            |
| 確認\_成功しました (hresult、\[省略可能なメッセージ\])                                          | 指定した HRESULT が成功したことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                            |
| 確認\_SUCCEEDED\_を返す (hresult、\[省略可能なメッセージ\])                                  | 指定した HRESULT が正常に完了し、マクロに渡された HRESULT を返すことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                     |
| 確認\_できませんでした (hresult、\[省略可能なメッセージ\])                                             | 指定した HRESULT が失敗したことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                        |
| 確認\_FAILED\_を返す (hresult、\[省略可能なメッセージ\])                                     | 指定した HRESULT が失敗し、マクロに渡された HRESULT を返すことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                 |
| 確認\_をスローします (操作、例外、\[省略可能なメッセージ\])                                | 指定された操作が特定の例外の種類をスローすることを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                        |
| 確認\_いいえ\_スロー (操作、\[省略可能なメッセージ\])                                        | 指定された操作が例外をスローしないことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                            |
| 確認\_WIN32\_SUCCEEDED (win32Result、\[省略可能なメッセージ\])                               | 指定した Win32 結果が成功したことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                           |
| 確認\_WIN32\_SUCCEEDED\_を返す (win32Result、\[省略可能なメッセージ\])                       | 指定した Win32 結果が成功し、マクロに渡された時間の長いを返すことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                       |
| 確認\_WIN32\_FAILED (win32Result、\[省略可能なメッセージ\])                                  | 指定した Win32 結果が失敗したことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                                                                              |
| 確認\_WIN32\_FAILED\_を返す (win32Result、\[省略可能なメッセージ\])                          | 指定した Win32 結果が失敗し、マクロに渡された時間の長いを返すことを確認します。 指定されている場合は、カスタム メッセージを記録します。                                                                          |
| 確認\_WIN32\_BOOL\_SUCCEEDED (win32Bool、\[省略可能なメッセージ\])                           | 指定した Win32 BOOL が成功したことを確認します (! = FALSE)。 検証に失敗した場合は、GetLastError() の結果を記録します。 指定されている場合は、カスタム メッセージを記録します。                                                     |
| 確認\_WIN32\_BOOL\_SUCCEEDED\_を返す (win32Bool、\[省略可能なメッセージ\])                   | 指定した Win32 BOOL が成功したことを確認します (! = FALSE) をマクロに渡されたブール値を返します。 検証に失敗した場合は、GetLastError() の結果を記録します。 指定されている場合は、カスタム メッセージを記録します。 |
| 確認\_WIN32\_BOOL\_FAILED (win32Bool、\[省略可能なメッセージ\])                              | 指定した Win32 BOOL が失敗したことを確認します (= = FALSE)。 GetLastError() の結果を記録しません。 指定されている場合は、カスタム メッセージを記録します。                                                                          |
| 確認\_WIN32\_BOOL\_FAILED\_を返す (win32Bool、\[省略可能なメッセージ\])                      | 指定した Win32 BOOL が失敗したことを確認します (= = FALSE) をマクロに渡されたブール値を返します。 GetLastError() の結果を記録しません。 指定されている場合は、カスタム メッセージを記録します。                      |



### <a name="span-idexceptioncplusplusspanspan-idexceptioncplusplusspanexception-based-verify-usage"></a><span id="exception_cplusplus"></span><span id="EXCEPTION_CPLUSPLUS"></span>ベースの例外は、使用状況を確認します。

ソース コードをコンパイルした C++ の例外を有効になっているかどうか (指定することで、"/EHsc"コマンド ライン スイッチ、または"使用\_ネイティブ\_EH = 1" ソース ファイル内のマクロ)、確認マクロは既定で失敗した場合、その後に、エラーを記録し、によってネイティブの C++ 例外をスローします。 スローされた例外、 **WEX::TestExecution::VerifyFailureException**します。 この例外をキャッチする必要はありません - TAEF フレームワークがそれをキャッチし、[次へ] のテスト_ケースに進みます。

一連の検証を実行したい場合は、テストのではなく、行が最初の検証エラーで中止、使用できます必要に応じて、 **DisableVerifyExceptions**クラス。 オブジェクトの有効期間は、例外が無効になっている時間の量を制御します。

```cpp
if (NULL != m_key)
{
    DisableVerifyExceptions disable;
    VERIFY_WIN32_SUCCEEDED(::RegDeleteKey(HKEY_CURRENT_USER, zTempName));
    VERIFY_WIN32_SUCCEEDED(::RegCloseKey(m_key));
}
```

上記の例では、例外が内でのみ無効、"場合 (NULL! = m\_キー)"ブロックや検証の 2 番目の呼び出しが行われても確認の最初の呼び出しに失敗した場合。

**DisableVerifyExceptions**クラスは、ref カウントであり、スレッドごとにも機能します。

### <a name="span-idnonexceptioncplusplusspanspan-idnonexceptioncplusplusspannon-exception-based-verify-usage"></a><span id="nonexception_cplusplus"></span><span id="NONEXCEPTION_CPLUSPLUS"></span>非例外ベースの使用状況を確認します。

場合は、ソース コードは***いない***C++ の例外を有効になっているとコンパイルされると、確認マクロはスローされませんネイティブ C++ の検証が失敗したときにします。 さらに、ソース コードをコンパイルした場合 C++ の例外を有効になっているが、単に、検証例外を無効にする\#定義なし\_確認\_"WexTestClass.h"を含める前に例外。

このモデルで行う必要があります、一連の入れ子になった if ステートメントは、テストのフローを制御するためにケースではなくより、C++ 例外に依存します。

```cpp
if (VERIFY_WIN32_SUCCEEDED(::RegDeleteKey(HKEY_CURRENT_USER, zTempName)))
{
    ...
}
```

### <a name="span-idoutsettingscplusplusspanspan-idoutsettingscplusplusspanverify-output-settings"></a><span id="outsettings_cplusplus"></span><span id="OUTSETTINGS_CPLUSPLUS"></span>出力の設定を確認します。

確認 Api によって生成された出力をカスタマイズする場合は、使用できます、 **SetVerifyOutput**クラス。 オブジェクトの有効期間は、出力設定が設定されている時間の量を制御します。 **SetVerifyOutput**クラスは、ref カウントであり、スレッドごとに機能します。

```cpp
if (NULL != m_key)
{
    SetVerifyOutput verifySettings(VerifyOutputSettings::LogOnlyFailures);
    VERIFY_IS_TRUE(true, L"Should NOT log a comment");
    VERIFY_IS_TRUE(false, L"Should log an error");
}
VERIFY_IS_TRUE(true, L"Should log a comment");
```

上記の例では、指定した設定のみに関連する内で行われた呼び出し、"場合 (NULL! = m\_キー)"ブロック、および*のみ*失敗した検証呼び出しをログに記録されます。 ただし、3 番目の確認の呼び出しが成功した場合でも記録されます。 これは、スコープ外に出て SetVerifyOutput クラスという事実が原因です。

検証出力を設定するため、次のオプションがあります。

<span id="VerifyOutputSettings__LogOnlyFailures_"></span><span id="verifyoutputsettings__logonlyfailures_"></span><span id="VERIFYOUTPUTSETTINGS__LOGONLYFAILURES_"></span>VerifyOutputSettings::LogOnlyFailures   
失敗しただけの呼び出しをログに記録されます。 を確認します。すべての成功した呼び出しは無視されます。

<span id="VerifyOutputSettings__LogFailuresAsBlocked_"></span><span id="verifyoutputsettings__logfailuresasblocked_"></span><span id="VERIFYOUTPUTSETTINGS__LOGFAILURESASBLOCKED_"></span>VerifyOutputSettings::LogFailuresAsBlocked   
すべてのエラーは、エラーをログ記録ではなくブロックとしてログインします。

<span id="VerifyOutputSettings__LogFailuresAsWarnings_"></span><span id="verifyoutputsettings__logfailuresaswarnings_"></span><span id="VERIFYOUTPUTSETTINGS__LOGFAILURESASWARNINGS_"></span>VerifyOutputSettings::LogFailuresAsWarnings   
すべてのエラー、エラーを記録するのではなく警告としてログに記録します。

<span id="VerifyOutputSettings__LogValuesOnSuccess_"></span><span id="verifyoutputsettings__logvaluesonsuccess_"></span><span id="VERIFYOUTPUTSETTINGS__LOGVALUESONSUCCESS_"></span>VerifyOutputSettings::LogValuesOnSuccess   
検証の呼び出しが成功した場合でも、渡されるパラメーターの値を記録します。

出力設定ができることを確認または複数の設定を有効にするまとめて必要があります。

```cpp
SetVerifyOutput verifySettings(VerifyOutputSettings::LogOnlyFailures | VerifyOutputSettings::LogFailuresAsBlocked);
```

### <a name="span-idoutcustomcplusplusspanspan-idoutcustomcplusplusspanproviding-value-output-for-custom-types"></a><span id="outcustom_cplusplus"></span><span id="OUTCUSTOM_CPLUSPLUS"></span>カスタムの型の値の出力の指定

C++ の検証フレームワークは、任意のカスタム型の詳細な出力を生成する機能を提供します。 そのために、1 つはの特殊化を実装する必要が、 **WEX::TestExecution::VerifyOutputTraits**クラス テンプレートです。

**WEX::TestExecution::VerifyOutputTraits**にクラス テンプレートの特殊化が存在する必要があります、 **WEX::TestExecution**名前空間。 というパブリック静的メソッドを提供することが想定されても**ToString**、し、クラスへの参照を受け取り、 **WEX::Common::NoThrowString**の値の文字列表現を含む.

```cpp
    class MyClass
    {
    public:
        MyClass(int value)
            : m_myValue(value)
        {
        }

        int GetValue()
        {
            return m_myValue;
        }

    private:
        int m_myValue;
    }

    namespace WEX { namespace TestExecution
    {
        template <>
        class VerifyOutputTraits<MyClass>
        {
        public:
            static WEX::Common::NoThrowString ToString(const MyClass& myClass)
            {
                return WEX::Common::NoThrowString().Format(L"%d", myClass.GetValue());
            }
        };
    }}
```

### <a name="span-idcomparatorscplusplusspanspan-idcomparatorscplusplusspanproviding-comparators-for-custom-types"></a><span id="comparators_cplusplus"></span><span id="COMPARATORS_CPLUSPLUS"></span>カスタム型の比較子を提供します。

C++ の確認、フレームワークを対応する演算子のオーバー ロードを実装しないカスタム型の比較子を定義する機能を提供します (演算子 =、演算子&lt;など)。 そのために、1 つはの特殊化を実装する必要が、 **WEX::TestExecution::VerifyCompareTraits**クラス テンプレートです。

**WEX::TestExecution::VerifyCompareTraits**にクラス テンプレートの特殊化が存在する必要があります、 **WEX::TestExecution**名前空間。 Public static を指定すると予想されても呼び出されるメソッド**AreEqual**、 **AreSame**、 **IsLessThan**、 **IsGreaterThan**、および**IsNull**します。

```cpp
    class MyClass
    {
    public:
        MyClass(int value)
            : m_myValue(value)
        {
        }

        int GetValue()
        {
            return m_myValue;
        }

    private:
        int m_myValue;
    }

    namespace WEX { namespace TestExecution
    {
        template <>
        class VerifyCompareTraits<MyClass, MyClass>
        {
        public:
            static bool AreEqual(const MyClass& expected, const MyClass& actual)
            {
                return expected.GetValue() == actual.GetValue();
            }

            static bool AreSame(const MyClass& expected, const MyClass& actual)
            {
                return &expected == &actual;
            }

            static bool IsLessThan(const MyClass& expectedLess, const MyClass& expectedGreater)
            {
                return (expectedLess.GetValue() < expectedGreater.GetValue());
            }

            static bool IsGreaterThan(const MyClass& expectedGreater, const MyClass& expectedLess)
            {
                return (expectedGreater.GetValue() > expectedLess.GetValue());
            }

            static bool IsNull(const MyClass& object)
            {
                return object.GetValue() == 0;
            }
        };
    }}
```

## <a name="span-idcsharpspanspan-idcsharpspanusing-verify-from-c"></a><span id="csharp"></span><span id="CSHARP"></span>使用して確認しますC#


C#確認の使用状況は c++ に似ています。 ただし、経由で提供されます、**かかえるします。TestExecution.Verify**クラス内に置かれている**Te.Managed.dll**します。

使用できる次の確認方法C#テスト。

| マクロ                                                                                       | 機能                                                                                                                                                                       |
|---------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| AreEqual (オブジェクトが必要です、実際のオブジェクト)                                                    | 2 つの指定したオブジェクトが等しいことを確認します。                                                                                                                                      |
| AreEqual (オブジェクトが必要です、実際のオブジェクト、文字列メッセージ)                                    | 2 つの指定したオブジェクトが等しいことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                            |
| AreEqual&lt;T&gt;(T 必要ですが、実際の T)                                                     | 2 つの指定したオブジェクトが等しいことを確認します。                                                                                                                                      |
| AreEqual&lt;T&gt;(予想 T、T 実際、文字列メッセージ)                                     | 2 つの指定したオブジェクトが等しいことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                            |
| AreNotEqual (オブジェクトが必要です、実際のオブジェクト)                                                 | 2 つの指定したオブジェクトが等しくないことを確認します。                                                                                                                                  |
| AreNotEqual (オブジェクトが必要です、実際のオブジェクト、文字列メッセージ)                                 | 2 つの指定したオブジェクトが等しくないことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                        |
| AreNotEqual&lt;T&gt;(T 必要ですが、実際の T)                                                  | 2 つの指定したオブジェクトが等しくないことを確認します。                                                                                                                                  |
| AreNotEqual&lt;T&gt;(予想 T、T 実際、文字列メッセージ)                                  | 2 つの指定したオブジェクトが等しくないことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                        |
| AreSame (オブジェクトが必要です、実際のオブジェクト)                                                     | 指定された 2 つのパラメーターが同じオブジェクトを参照していることを確認します。                                                                                                                |
| AreSame (オブジェクトが必要です、実際のオブジェクト、文字列メッセージ)                                     | 指定された 2 つのパラメーターが同じオブジェクトを参照していることを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                      |
| AreNotSame (オブジェクトが必要です、実際のオブジェクト)                                                  | 指定された 2 つのパラメーターが同じオブジェクトを参照しないことを確認します。                                                                                                         |
| AreNotSame (オブジェクトが必要です、実際のオブジェクト、文字列メッセージ)                                  | 指定された 2 つのパラメーターが同じオブジェクトを参照しないことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                               |
| IsGreaterThan (IComparable expectedGreater、IComparable expectedLess)                        | 最初のパラメーターが 2 番目のパラメーターより大きいことを確認します。                                                                                                             |
| IsGreaterThan (IComparable expectedGreater、IComparable expectedLess、文字列メッセージ)        | 最初のパラメーターが 2 番目のパラメーターより大きいことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                   |
| IsGreaterThanOrEqual (IComparable expectedGreater、IComparable expectedLess)                 | 最初のパラメーターが 2 番目のパラメーター以上であることを確認します。                                                                                                 |
| IsGreaterThanOrEqual (IComparable expectedGreater、IComparable expectedLess、文字列メッセージ) | 最初のパラメーターが 2 番目のパラメーター以上であることを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                       |
| IsLessThan (IComparable expectedLess、IComparable expectedGreater)                           | 最初のパラメーターが小さいことを確認します。 2 番目のパラメーターよりもします。                                                                                                                |
| IsLessThan (IComparable expectedLess、IComparable expectedGreater、文字列メッセージ)           | 最初のパラメーターが小さいことを確認します 2 番目のパラメーターよりも。検証の成功または失敗時にカスタム メッセージを記録します。                                                      |
| IsLessThanOrEqual (IComparable expectedLess、IComparable expectedGreater)                    | 最初のパラメーターが 2 番目のパラメーター以下であることを確認します。                                                                                                    |
| IsLessThanOrEqual (IComparable expectedLess、IComparable expectedGreater、文字列メッセージ)    | 最初のパラメーターは、2 番目のパラメーター以下のことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                          |
| 失敗 (文字列メッセージ)                                                                        | 条件を確認しないで失敗します。                                                                                                                                              |
| IsTrue (bool 条件)                                                                      | 指定した条件が true であることを確認します。                                                                                                                                      |
| IsTrue (bool 条件、文字列メッセージ)                                                      | 指定した条件が true であることを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                            |
| IsFalse (bool 条件)                                                                     | 指定した条件が false であることを確認します。                                                                                                                                     |
| IsFalse (bool 条件、文字列メッセージ)                                                     | 指定した条件が false 以外であることを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                           |
| IsNull(object obj)                                                                          | 指定されたパラメーターが NULL であることを確認します。                                                                                                                                      |
| IsNull(object obj, string message)                                                          | 指定されたパラメーターが NULL であることを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                            |
| IsNotNull(object obj)                                                                       | 指定されたパラメーターが NULL でないことを確認します。                                                                                                                                  |
| IsNotNull(object obj, string message)                                                       | 指定されたパラメーターが NULL 以外でないことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                                        |
| スロー&lt;T&gt;(VerifyOperation 操作)                                                  | 指定された操作が特定の例外の種類をスローすることを確認します。 例外をさらなる調査を返します。                                                           |
| スロー&lt;T&gt;(VerifyOperation 操作、文字列メッセージ)                                  | 指定された操作が特定の例外の型をスローすることを確認します。検証の成功または失敗時にカスタム メッセージを記録します。 例外をさらなる調査を返します。 |
| NoThrow (VerifyOperation 操作)                                                          | 指定された操作が例外をスローしないことを確認します。                                                                                                                  |
| NoThrow (VerifyOperation 操作、文字列メッセージ)                                          | 指定された操作が例外をスローしないことを確認します。検証の成功または失敗時にカスタム メッセージを記録します。                                                        |



### <a name="span-idexceptioncsharpspanspan-idexceptioncsharpspanexception-based-verify-usage"></a><span id="exception_csharp"></span><span id="EXCEPTION_CSHARP"></span>ベースの例外は、使用状況を確認します。

検証エラーが発生した場合C#テストの場合、エラーは、logger に書き込まれます。、**かかえるします。TestExecution.VerifyFailureException**がスローされます。 ネイティブの C++ モデルと同じようにこれらの例外をキャッチについて心配する必要はありません。 TAEF フレームワークがそれをキャッチし、[次へ] のテスト_ケース移動します。

一連の検証を実行したい場合は、テストのではなく、行が最初の検証エラーで中止、使用できます必要に応じて、 **DisableVerifyExceptions**クラス。 オブジェクトの有効期間は、例外が無効になっている時間の量を制御します。 **DisableVerifyExceptions**クラスは、ref カウントであり、スレッドごとに機能します。

```cpp
using (new DisableVerifyExceptions())
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
```

上記の例で確認の最初の呼び出しに失敗した場合、2 番目を確認してください呼び出しは引き続き行われます。

または、設定して同じ結果を得ることができます**Verify.DisableVerifyExceptions = true**などは、次に示す例では、検証操作の前にします。

```cpp
Verify.DisableVerifyExceptions = true;
try
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
finally
{
    Verify.DisableVerifyExceptions = false;
}
```

このようなオプションが使用可能なを使用して、オブジェクトとして DisableVerifyExeptions を宣言する場合でもブロックは、まだことをお勧めに注意してください。

検証エラーが発生する例外ダイアログ ボックス (Ctrl + Alt + E) を表示、デバッガーで停止する場合は、[追加] をクリックして、ドロップダウン リストに"Common Language Runtime Exceptions"を選択して、"かかえるします。[名前] フィールドで"TestExecution.VerifyFailureException します。

### <a name="span-idoutsettingscsharpspanspan-idoutsettingscsharpspanverify-output-settings"></a><span id="outsettings_csharp"></span><span id="OUTSETTINGS_CSHARP"></span>出力の設定を確認します。

確認 Api によって生成された出力をカスタマイズする場合は、使用できます、 **SetVerifyOutput**クラス。 オブジェクトの有効期間は、出力設定が設定されている時間の量を制御します。 **SetVerifyOutput**クラスは、ref カウントであり、スレッドごとに機能します。

```cpp
using (new SetVerifyOutput(VerifyOutputSettings.LogOnlyFailures))
{
    Log.Comment("Only the following error should be logged:");
    Verify.IsTrue(true, "Should NOT log a comment");
    Verify.IsTrue(false, "Should log an error");
}
Verify.IsTrue(true, "Should log a comment");
```

使用して、失敗する唯一の呼び出しであるために、2 番目の確認の呼び出しのみが記録される上記の例では、ブロックします。 ただし、3 つ目は呼び出しを確認します。*は*成功した場合でもログに記録します。 これは、スコープ外に出て SetVerifyOutput クラスという事実が原因です。

または、設定して同じ結果を得ることができます**Verify.OutputSettings = VerifyOutputSettings.LogOnlyFailures**などは、次に示す例では、検証操作の前にします。

```cpp
Verify.OutputSettings = VerifyOutputSettings.LogFailuresAsWarnings
try
{
    Verify.AreSame(item1, item2);
    Verify.AreEqual(item1, item2);
}
finally
{
    Verify.OutputSettings = VerifyOutputSettings.None;
}
```

このようなオプションが使用可能なを使用して、オブジェクトとして SetVerifyOutput を宣言する場合でもブロックは、まだことをお勧めに注意してください。

検証出力を設定するため、次のオプションがあります。

<span id="verifyoutputsettings.logonlyfailures_"></span><span id="VERIFYOUTPUTSETTINGS.LOGONLYFAILURES_"></span>VerifyOutputSettings.LogOnlyFailures   
失敗しただけの呼び出しをログに記録されます。 を確認します。すべての成功した呼び出しは無視されます。

<span id="verifyoutputsettings.logfailuresasblocked_"></span><span id="VERIFYOUTPUTSETTINGS.LOGFAILURESASBLOCKED_"></span>VerifyOutputSettings.LogFailuresAsBlocked   
すべてのエラーは、エラーをログ記録ではなくブロックとしてログインします。

<span id="verifyoutputsettings.logfailuresaswarnings_"></span><span id="VERIFYOUTPUTSETTINGS.LOGFAILURESASWARNINGS_"></span>VerifyOutputSettings.LogFailuresAsWarnings   
すべてのエラー、エラーを記録するのではなく警告としてログに記録します。

出力設定ができることを確認または複数の設定を有効にするまとめて必要があります。

```cpp
using (new SetVerifyOutput(VerifyOutputSettings.LogFailuresAsBlocked | VerifyOutputSettings.LogOnlyFailures))
{
...
}
```

## <a name="span-idscriptspanspan-idscriptspanusing-verify-from-script"></a><span id="script"></span><span id="SCRIPT"></span>スクリプトから使用して確認します


C++ として同じ使用パターンを次のスクリプト言語では、検証 API が提示されるもとC#します。

### <a name="span-idinstallationspanspan-idinstallationspanspan-idinstallationspaninstallation"></a><span id="Installation"></span><span id="installation"></span><span id="INSTALLATION"></span>インストール

API の使用、スクリプト可能なことを確認するときから TAEF テスト メソッド内でのインストールは必要ありません - ' の登録を必要としない COM' を使用して、必要な API が登録されます。 TAEF テストの範囲外から可能な API を使用するにはメソッド (TAEF、外部または子プロセス) 登録するだけです。 管理者特権でコマンド プロンプトから regsvr32 を使用して、Te.Common.dll バイナリ例えば：

``` syntax
regsvr32 Te.Common.dll
```

ラボの実行の配置ファイルを使用して TAEF をデプロイするときに Te.Common.dll は自動的に登録します。

### <a name="span-idusagescriptspanspan-idusagescriptspanusage"></a><span id="usage_script"></span><span id="USAGE_SCRIPT"></span>使用状況

スクリプトを作成できることを確認 API の 'TE.Common.Verify' COM クラスに表示されます - クラスと呼び出しのメソッドも検証クラスが自動的にで動作するパスを作成し、ログに検証が失敗する WEXLogger を単純にインスタンス化します。

```cpp
1   <?xml version="1.0" ?>
2   <?component error="false" debug="false"?>
3   <package>
4     <component id="Example">
5       <object id="Log" progid="Wex.Logger.Log" />
6       <object id="Verify" progid="Te.Common.Verify" />
7       <reference guid="e65ef678-a232-42a7-8a36-63108d719f31" version="1.0"/>
8       <reference guid="f8bb9db9-e54e-4555-b3e5-e3ddf2fef401" version="1.0"/>
9
10      <public>
11        <method name="HelloWorld"/>
12      </public>
13
14      <script language="JScript">
15          function HelloWorld() {
16              Verify.IsTrue(true);
17              Verify.IsFalse(false);
18          }
19      </script>
20    </component>
21  </package>
```

この例では、単一の"hello World"メソッドと TAEF スクリプトのテスト クラスを定義します。 6 行目では、'object' 要素を使用して、グローバル スコープで確認してください変数を定義します。 8 行目では、'reference' 要素を使用して、スクリプトのグローバル スコープに (この例では、Te.Common.dll のタイプ ライブラリ) で指定されたタイプ ライブラリからすべての定数を含めるここで 'VerifySettings' の定数を追加します。 16 ~ 17 行目では、確認 API の使用量だけを表示します。 実行すると、例では、次の出力が生成されます。

``` syntax
Test Authoring and Execution Framework v2.7 Build 6.2.7922.0 (fbl_esc_end_dev(mschofie).110202-1000) For x86

StartGroup: Example::HelloWorld
Verify: IsTrue
Verify: IsFalse
EndGroup: Example::HelloWorld [Passed]

Summary: Total=1, Passed=1, Failed=0, Blocked=0, Not Run=0, Skipped=0
```

### <a name="span-idapiscriptspanspan-idapiscriptspanscriptable-verify-api"></a><span id="api_script"></span><span id="API_SCRIPT"></span>スクリプト可能な API を確認します。

スクリプトを作成できることを確認 API での検証メソッドは次のとおりです。

| メソッド                                                                                | 機能                                                                                                                                                                                                                                                                                                                  |
|---------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| bool Verify.AreEqual (予想される、実際、\[省略可能なメッセージ\])                          | 2 つの値が等しいことを確認します。 場合、' VerifySettings\_CoerceTypes の設定を有効に、このメソッドは、場合に等しいかどうかの JScript の定義を使用して、' VerifySettings\_CoerceTypes の設定が有効になっていない、メソッドは id の JScript の定義を使用します。 **' VerifySettings\_CoerceTypes' が既定でオンです。**     |
| bool Verify.AreNotEqual (予想される、実際、\[省略可能なメッセージ\])                       | 2 つの値が等しいがないことを確認します。 場合、' VerifySettings\_CoerceTypes の設定を有効に、このメソッドは、場合に等しいかどうかの JScript の定義を使用して、' VerifySettings\_CoerceTypes の設定が有効になっていない、メソッドは id の JScript の定義を使用します。 **' VerifySettings\_CoerceTypes' が既定でオンです。** |
| bool Verify.IsGreaterThan (expectedGreater、expectedLess、\[省略可能なメッセージ\])        | 最初の値が 2 番目より大きいことを確認します。                                                                                                                                                                                                                                                                      |
| bool Verify.IsGreaterThanOrEqual (expectedGreater、expectedLess、\[省略可能なメッセージ\]) | 最初の値がもう 1 つ以上のことを確認します。                                                                                                                                                                                                                                                          |
| bool Verify.IsLessThan (expectedLess、expectedGreater、\[省略可能なメッセージ\])           | 最初の値が小さいことを確認します。 2 番目より。                                                                                                                                                                                                                                                                         |
| bool Verify.IsLessThanOrEqual (expectedLess、expectedGreater、\[省略可能なメッセージ\])    | 最初の値が 2 番目に小さいことを確認します。                                                                                                                                                                                                                                                             |
| bool Verify.AreSame (予想される、実際、\[省略可能なメッセージ\])                           | 値が同じであることを検証します。                                                                                                                                                                                                                                                                                         |
| bool Verify.AreNotSame (予想される、実際、\[省略可能なメッセージ\])                        | 値がない同じことを確認します。                                                                                                                                                                                                                                                                                     |
| bool Verify.Fail (\[省略可能なメッセージ\])                                                | 条件をチェックせずに失敗します。                                                                                                                                                                                                                                                                                             |
| bool Verify.IsTrue (式、\[省略可能なメッセージ\])                                  | 指定された式が true に評価されたことを確認します。                                                                                                                                                                                                                                                                          |
| bool Verify.IsFalse(expression, \[optional message\])                                 | 指定された式が false に評価されることを確認します。                                                                                                                                                                                                                                                                         |
| bool Verify.IsNull (必要ですが、\[省略可能なメッセージ\])                                    | 指定された値が 'null' であることを確認します。                                                                                                                                                                                                                                                                                       |
| bool Verify.IsNotNull(expected, \[optional message\])                                 | 指定された値が 'null' でないことを確認します。                                                                                                                                                                                                                                                                                   |
| bool Verify.Throws (関数、\[省略可能なメッセージ\])                                    | 指定された関数がスローすることを確認し、例外。                                                                                                                                                                                                                                                                         |
| bool Verify.NoThrow (関数、\[省略可能なメッセージ\])                                   | 指定された関数がスローしないことを確認し、例外。                                                                                                                                                                                                                                                                 |



設定を制御するため、検証クラスでは、2 つの方法があります。

| メソッド                                  | 機能                                         |
|-----------------------------------------|-------------------------------------------------------|
| Verify.EnableSettings(settings) オブジェクト  | 指定したフラグまたはフラグの設定が有効になります。  |
| Verify.DisableSettings(settings) オブジェクト | 指定したフラグまたはフラグの設定が無効になります。 |



Verify.EnableSettings または Verify.DisableSettings メソッドに渡される設定の値には、次の値のいずれかを指定できます。

<span id="VerifySettings_LogOnlyFailures___0x01"></span><span id="verifysettings_logonlyfailures___0x01"></span><span id="VERIFYSETTINGS_LOGONLYFAILURES___0X01"></span>VerifySettings\_LogOnlyFailures = 0x01  
エラーが記録 - に出力がないだけで成功を確認してくださいを呼び出します。

<span id="VerifySettings_LogFailuresAsBlocked___0x02"></span><span id="verifysettings_logfailuresasblocked___0x02"></span><span id="VERIFYSETTINGS_LOGFAILURESASBLOCKED___0X02"></span>VerifySettings\_LogFailuresAsBlocked 0x02 を =  
エラーは、「エラー」が既定ではなく 'ブロックされている'、として記録されます。

<span id="VerifySettings_LogFailuresAsWarnings___0x04"></span><span id="verifysettings_logfailuresaswarnings___0x04"></span><span id="VERIFYSETTINGS_LOGFAILURESASWARNINGS___0X04"></span>VerifySettings\_LogFailuresAsWarnings = 0x04  
エラーは、「エラー」が既定ではなく、「警告」として記録されます。

<span id="VerifySettings_LogValuesOnSuccess___0x08"></span><span id="verifysettings_logvaluesonsuccess___0x08"></span><span id="VERIFYSETTINGS_LOGVALUESONSUCCESS___0X08"></span>VerifySettings\_LogValuesOnSuccess = 0x08  
確認するパラメーターの値は、確認のログ メッセージの一部として書き込まれます。 **これは、既定でです。**

<span id="VerifySettings_CoerceTypes___0x1000"></span><span id="verifysettings_coercetypes___0x1000"></span><span id="VERIFYSETTINGS_COERCETYPES___0X1000"></span>VerifySettings\_CoerceTypes = 0x1000  
Verify メソッドに渡される値は、次の JScript の強制適用ルール強制的に変換されます。 **これは、既定でです。**

<span id="VerifySettings_DisableExceptions___0x2000"></span><span id="verifysettings_disableexceptions___0x2000"></span><span id="VERIFYSETTINGS_DISABLEEXCEPTIONS___0X2000"></span>VerifySettings\_DisableExceptions 0x2000 を =  
検証が失敗したときに、例外はスローされません。

### <a name="span-idsettingsscriptspanspan-idsettingsscriptspanverify-settings"></a><span id="settings_script"></span><span id="SETTINGS_SCRIPT"></span>設定を確認します

確認 API では、その動作を構成する設定を提供します。 有効または検証クラスを保持する特定の設定を無効にするには、'EnableSettings' と 'DisableSettings' メソッドを使用できます。 メソッドは、有効または無効にする 1 つまたは複数の設定を受け取ります。

```cpp
    Verify.EnableSettings(VerifySettings_LogOnlyFailures);
```

を有効にまたは 1 回の呼び出しで複数の設定を無効にするには、複数の 'VerifySettings' フラグを含めることができます。

```cpp
    Verify.EnableSettings(VerifySettings_LogOnlyFailures | VerifySettings_DisableExceptions);
```

EnableSettings と DisableSettings メソッドは、特定のスコープの設定を有効または無効にすることができます、元の設定を復元するために使用できるオブジェクトを返す

```cpp
1    var guard = Verify.EnableSettings(VerifySettings_LogOnlyFailures);
2    try
3    {
4        Verify.AreEqual(10, 0xa);
5    }
6    finally
7    {
8        guard.Restore();
9    }
```

この例では、Verify.EnableSettings メソッドに渡されます ' VerifySettings\_LogOnlyFailures' が既に確認オブジェクト上に存在する設定を使用するが組み込まれます。 Try-finally ブロック内で検証の呼び出しが行われたように中に、finally ブロックで、'guard' オブジェクトは、元の設定を復元するために使用できます。

### <a name="span-idexceptionscriptspanspan-idexceptionscriptspanexception-based-verify-usage"></a><span id="exception_script"></span><span id="EXCEPTION_SCRIPT"></span>ベースの例外は、使用状況を確認します。

既定では、確認、検証に失敗したときに、メソッドは例外をスローします。 テスト メソッドから例外がスローされる場合は、TAEF で実行されている、ときに、テストは失敗します。 次に、例を示します。

```cpp
1    var guard = Verify.EnableSettings(VerifySettings_CoerceTypes);
2    try
3    {
4        Verify.AreEqual(1, "1");
5        Verify.AreEqual("1", 1);
6    }
7    finally
8    {
9        guard.Restore();
10   }
```

この例では、2 番目の検証呼び出し決して行われる可能性が、最初は例外をスローし、テストに失敗するため。 失敗した検証スローしないでください、確認以降にすることを許可するように、この動作を変更することを確認 API の設定のサポートを使用できます。 これは、パラメーターのセットを確認することの検証にすべての書き込みかどうかを確認してに特に便利です。

```cpp
1    var guard = Verify.EnableSettings(VerifySettings_CoerceTypes | VerifySettings_DisableExceptions);
2    try
3    {
4        Verify.AreEqual(1, "1");
5        Verify.AreEqual("1", 1);
6    }
7    finally
8    {
9        guard.Restore();
10   }
```

例外が無効になっているために、両方の検証は、ログに書き込まれます。

### <a name="span-idoutsideapiscriptspanspan-idoutsideapiscriptspanusing-the-scriptable-verify-api-outside-taef"></a><span id="outsideapi_script"></span><span id="OUTSIDEAPI_SCRIPT"></span>API の外部 TAEF、スクリプトを使用して確認します

TAEF 外部スクリプトを作成できることを確認 API を使用できます。 Te.Common.dll が登録されていることを確認してください、[インストール セクション](#installation)、シンプルな"TE.Common.Verify"クラスを作成します。

```cpp
var VerifySettings_DisableExceptions = 0x2000;

var Verify = new ActiveXObject("TE.Common.Verify");
var Log = new ActiveXObject("WEX.Logger.Log");

Verify.EnableSettings(VerifySettings_DisableExceptions);

Log.StartGroup("Group A");
Verify.AreEqual(1, 2);
Log.EndGroup("Group A");

Log.StartGroup("Group B");
Verify.AreEqual(2, 2);
Log.EndGroup("Group B");
```

フォロー コンソール出力が cscript で実行されたときに、上記のコードが生成されます。

``` syntax
StartGroup: Group A
Error: Verify: AreEqual - Values (1, 2)
EndGroup: Group A [Failed]

StartGroup: Group B
Verify: AreEqual - Values (2, 2)
EndGroup: Group B [Passed]

Non-passing Tests:

    Group A [Failed]

Summary: Total=2, Passed=1, Failed=1, Blocked=0, Not Run=0, Skipped=0
```

[' かかえるします。Logger.Log' API](wexlogger.md) (たとえば、子プロセスの場合) として、必要に応じてかかえるロガーを構成するために使用して、その構成のスクリプトを作成できることを確認 API が利用されます。









