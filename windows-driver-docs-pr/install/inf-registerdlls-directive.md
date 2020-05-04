---
title: INF RegisterDlls ディレクティブ
description: RegisterDlls ディレクティブは、OLE コントロールであり、自己登録が必要なファイルを指定するために使用される1つ以上の INF セクションを参照します。
ms.assetid: 59da13e6-f801-4efe-8cd3-d0305e503c24
keywords:
- INF RegisterDlls ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF RegisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ef1e5c3a53b07c958f26fa525d3aa7899ea3c39
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223096"
---
# <a name="inf-registerdlls-directive"></a>INF RegisterDlls ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 [Reg2inf ツール](../devtest/reg2inf.md)を使用すると、ドライバーパッケージを universal にするために、既存の[inf Registerdlls ディレクティブ](../install/inf-registerdlls-directive.md)を[inf AddReg ディレクティブ](../install/inf-addreg-directive.md)に変換できます。  詳細については、「 [UNIVERSAL INF ファイルの使用](using-a-universal-inf-file.md)」を参照してください。

**Registerdlls**ディレクティブは、OLE コントロールであり、自己登録が必要なファイルを指定するために使用される1つ以上の INF セクションを参照します。

```inf
[DDInstall]
  
RegisterDlls=register-dll-section[,register-dll-section]...
```

**Registerdlls**ディレクティブによって参照される各 INF セクションは、次のエントリ形式である必要があります。

```inf
[register-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

*登録 dll セクション*には、任意の数のエントリを含めることができます。各エントリは個別の行にあります。

## <a name="entries"></a>エントリ


<a href="" id="dirid"></a>*dirid*  
登録するファイルの保存先ディレクトリ ID を指定します。 詳細については、「 [Dirids の使用](using-dirids.md)」を参照してください。

<a href="" id="subdir"></a>*subdir*  
登録するファイルへのディレクトリパスを、現在のディレクトリを基準として指定します。 指定しない場合、ファイルは現在のディレクトリにあります。

<a href="" id="filename"></a>*/db*  
登録する OLE コントロールのファイル名を指定します。

<a href="" id="registration-flags"></a>*登録-フラグ*  
OLE コントロールに対して実行する登録操作を示します。 次のフラグの一方または両方を指定する必要があります。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)  
Windows SDK のドキュメントで説明されているように、OLE コントロールの**DllRegisterServer**関数を呼び出します。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)   
Windows SDK のドキュメントで説明されているように、OLE コントロールの**DllInstall**関数を呼び出します。

<a href="" id="timeout"></a>*タイムアウト*  
OLE コントロールが指定された登録呼び出しを完了するためのタイムアウト (秒単位) を指定します。 既定のタイムアウトは60秒です。

<a href="" id="argument"></a>*引数*  
コントロールが実行可能ファイルの場合、これは実行可能ファイルに渡されるコマンド文字列です。 既定の引数は**指定できませ**ん。

コントロールが実行可能ファイルでない場合は、 **DllInstall**関数に渡すコマンドライン引数を指定します。

<a name="remarks"></a>解説
-------

各*登録 dll セクション*名は、INF ファイルに対して一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

次の規則は、デバイスのインストールに**Registerdlls**ディレクティブを使用する場合に適用されます。

-   この構文では、ファイル名を DLL または実行可能ファイルのいずれかにすることができますが、デバイスをインストールする場合は DLL のみが許可されます。
-   登録するコードでは、ユーザー入力を求めるメッセージを表示しません。
-   サーバー側のインストールは、システムコンテキストで実行されます。 そのため、登録されているコードにセキュリティの脆弱性が含まれていないこと、およびファイルのアクセス許可によってコードが故意に変更されないようにする必要があります。

OLE コントロールと自己登録の詳細については、Windows SDK のドキュメントを参照してください。

<a name="examples"></a>例
--------

```inf
[Dialer]
RegisterDlls = DialerRegSvr
[DialerUninstall]
UnregisterDlls = DialerRegSvr
[DialerRegSvr]
11,,avtapi.dll, 1
```

## <a name="see-also"></a>関連項目


[**UnregisterDlls**](inf-unregisterdlls-directive.md)

 

 






