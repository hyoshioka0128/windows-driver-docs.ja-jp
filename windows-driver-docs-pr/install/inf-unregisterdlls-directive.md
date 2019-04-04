---
title: INF UnregisterDlls ディレクティブ
description: UnregisterDlls ディレクティブは、OLE コントロールは、(自己の削除) を自己登録解除を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。
ms.assetid: 11d29c7f-9bd8-4097-9842-ce7431389241
keywords:
- INF UnregisterDlls ディレクティブ デバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF UnregisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c015891175f687d8035116efa48e5a30e2e170a6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56579350"
---
# <a name="inf-unregisterdlls-directive"></a>INF UnregisterDlls ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバー パッケージを作成している場合は、このディレクティブが無効です。 参照してください[ユニバーサル INF ファイルを使用して](using-a-universal-inf-file.md)します。

 

**UnregisterDlls**ディレクティブが OLE コントロールは、(自己の削除) を自己登録解除を必要とするファイルを指定するために使用する 1 つまたは複数の INF セクションを参照します。

```ini
[DDInstall]
  
UnregisterDlls=unregister-dll-section[,unregister-dll-section]...
```

によって参照される各 INF セクション、 **UnregisterDlls**ディレクティブは、次のエントリの形式である必要があります。

```ini
[unregister-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

*の登録を解除 dll セクション*それぞれ別々 の行に任意の数のエントリを持つことができます。

## <a name="entries"></a>エントリ


<a href="" id="dirid"></a>*Dirid*  
登録解除するファイルの変換先のディレクトリ ID を指定します。 詳細については、[を使用して Dirids](using-dirids.md)を参照してください。

<a href="" id="subdir"></a>*subdir*  
登録解除するファイルを現在のディレクトリに対する相対パスを指定します。 指定されていない場合、ファイルは、現在のディレクトリです。

<a href="" id="filename"></a>*ファイル名*  
登録解除する OLE コントロールのファイル名を識別します。

<a href="" id="registration-flags"></a>*登録フラグ*  
OLE コントロールで実行する登録操作を示します。 次のフラグの一方または両方を指定する必要があります。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)  
呼び出す、 **DllUnRegisterServer**関数 (Windows SDK のドキュメントで説明)。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)   
呼び出す OLE コントロールの**DllInstall**関数 (Windows SDK のドキュメントで説明)。

<a href="" id="timeout"></a>*タイムアウト*  
指定した登録解除の呼び出しを完了する OLE コントロールの秒単位で、タイムアウトを指定します。 既定のタイムアウトは、60 秒です。

<a href="" id="argument"></a>*引数*  
コントロールが実行可能ファイルの場合は、これは、実行可能ファイルに渡されるコマンド文字列になります。 既定の引数は **/UnRegServer**します。

コントロールが実行可能ファイルでない場合に渡すコマンドライン引数を指定します、 **DllInstall**関数。

<a name="remarks"></a>コメント
-------

各*の登録を解除 dll セクション*名は、INF ファイルに一意である必要があり、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、[INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)を参照してください。

OLE コントロールと自己登録を解除する方法の詳細については、Windows SDK のドキュメントを参照してください。

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


[**RegisterDlls**](inf-registerdlls-directive.md)

 

 






