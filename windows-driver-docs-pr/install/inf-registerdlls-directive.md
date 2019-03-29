---
title: INF RegisterDlls ディレクティブ
description: RegisterDlls ディレクティブは、OLE コントロールは、自己登録を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。
ms.assetid: 59da13e6-f801-4efe-8cd3-d0305e503c24
keywords:
- INF RegisterDlls ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF RegisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 89ec7c7fe0ad0ac159c2cbfad20016c06b3895f8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572109"
---
# <a name="inf-registerdlls-directive"></a>INF RegisterDlls ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 使用することができます、 [Reg2inf ツール](../devtest/reg2inf.md)既存を変換する[INF RegisterDlls ディレクティブ](../install/inf-registerdlls-directive.md)に[INF AddReg ディレクティブ](../install/inf-addreg-directive.md)ユニバーサル ドライバー パッケージを作成するためにします。  詳細については、次を参照してください。[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

A **RegisterDlls**ディレクティブが OLE コントロールは、自己登録を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。

```ini
[DDInstall]
  
RegisterDlls=register-dll-section[,register-dll-section]...
```

によって参照される各 INF セクション、 **RegisterDlls**ディレクティブは、次のエントリの形式である必要があります。

```ini
[register-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

A*レジスタ-section dll*それぞれ別々 の行に任意の数のエントリを持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="dirid"></a>*Dirid*  
登録するファイルの変換先のディレクトリ ID を指定します。 詳細については、次を参照してください。[を使用して Dirids](using-dirids.md)します。

<a href="" id="subdir"></a>*subdir*  
登録するファイルを現在のディレクトリに対する相対のディレクトリ パスを指定します。 指定されていない場合、ファイルは、現在のディレクトリです。

<a href="" id="filename"></a>*ファイル名*  
登録する OLE コントロールのファイル名を識別します。

<a href="" id="registration-flags"></a>*登録フラグ*  
OLE コントロールで実行する登録操作を示します。 次のフラグの一方または両方を指定する必要があります。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)  
呼び出す OLE コントロールの**DllRegisterServer**関数 (Windows SDK のドキュメントで説明)。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)   
呼び出す OLE コントロールの**DllInstall**関数 (Windows SDK のドキュメントで説明)。

<a href="" id="timeout"></a>*タイムアウト*  
指定した登録呼び出しを完了する OLE コントロールの秒単位で、タイムアウトを指定します。 既定のタイムアウトは、60 秒です。

<a href="" id="argument"></a>*引数*  
コントロールが実行可能ファイルの場合は、これは、実行可能ファイルに渡されるコマンド文字列になります。 既定の引数は **/RegServer**します。

コントロールが実行可能ファイルでない場合に渡すコマンドライン引数を指定します、 **DllInstall**関数。

<a name="remarks"></a>コメント
-------

各*レジスタ-section dll*名は、INF ファイルに一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、次を参照してください。 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)します。

次の規則の使用に適用されます、 **RegisterDlls**ディレクティブをデバイスのインストール。

-   構文では、ファイル名を DLL または実行可能ファイルのいずれかにできますが、デバイスのインストールのみの DLL を使用できます。
-   ユーザーの入力を登録するコードを表示する必要があります。
-   サーバー側のインストールは、システム コンテキストで実行します。 そのため、非常に登録されているコードに記述されているセキュリティの脆弱性が含まれていないと、ファイルのアクセス許可が変更される悪意からコードを禁止することを確認する必要があります。

OLE コントロールと自己登録する方法の詳細については、Windows SDK のドキュメントを参照してください。

<a name="examples"></a>使用例
--------

```ini
[Dialer]
RegisterDlls = DialerRegSvr
[DialerUninstall]
UnregisterDlls = DialerRegSvr
[DialerRegSvr]
11,,avtapi.dll, 1
```

## <a name="see-also"></a>関連項目


[**UnregisterDlls**](inf-unregisterdlls-directive.md)

 

 






