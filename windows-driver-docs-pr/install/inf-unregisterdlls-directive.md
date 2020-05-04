---
title: INF UnregisterDlls ディレクティブ
description: UnregisterDlls ディレクティブは、OLE コントロールであり、自己登録解除 (自己削除) を必要とするファイルを指定するために使用される1つ以上の INF セクションを参照します。
ms.assetid: 11d29c7f-9bd8-4097-9842-ce7431389241
keywords:
- INF UnregisterDlls ディレクティブデバイスとドライバーのインストール
topic_type:
- apiref
api_name:
- INF UnregisterDlls Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 171c09d7f432d20853dd65e9a5c395808a1808e7
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223086"
---
# <a name="inf-unregisterdlls-directive"></a>INF UnregisterDlls ディレクティブ


**注**  ユニバーサルまたはモバイルのドライバーパッケージをビルドする場合、このディレクティブは無効です。 「[ユニバーサル INF ファイルの使用」を](using-a-universal-inf-file.md)参照してください。

 

**Unregisterdlls**ディレクティブは、OLE コントロールであり、自己登録解除 (自己削除) を必要とするファイルを指定するために使用される1つ以上の INF セクションを参照します。

```inf
[DDInstall]
  
UnregisterDlls=unregister-dll-section[,unregister-dll-section]...
```

**Unregisterdlls**ディレクティブによって参照される各 INF セクションは、次のエントリ形式である必要があります。

```inf
[unregister-dll-section] 
  
dirid,[subdir],filename,registration-flags[,[timeout][,argument]] 
```

*登録解除 dll セクション*には、任意の数のエントリを含めることができます。それぞれ個別の行になります。

## <a name="entries"></a>エントリ


<a href="" id="dirid"></a>*dirid*  
登録を解除するファイルの保存先ディレクトリ ID を指定します。 詳細については、「 [Dirids の使用](using-dirids.md)」を参照してください。

<a href="" id="subdir"></a>*subdir*  
登録を解除するファイルへの、現在のディレクトリを基準とした相対ディレクトリパスを指定します。 指定しない場合、ファイルは現在のディレクトリにあります。

<a href="" id="filename"></a>*/db*  
登録を解除する OLE コントロールのファイル名を指定します。

<a href="" id="registration-flags"></a>*登録-フラグ*  
OLE コントロールに対して実行する登録操作を示します。 次のフラグの一方または両方を指定する必要があります。

<a href="" id="0x00000001--flg-regsvr-dllregister-"></a>**0x00000001** (FLG_REGSVR_DLLREGISTER)  
Windows SDK のドキュメントで説明されているように、 **DllUnRegisterServer**関数を呼び出します。

<a href="" id="0x00000002--flg-regsvr-dllinstall--"></a>**0x00000002** (FLG_REGSVR_DLLINSTALL)   
Windows SDK のドキュメントで説明されているように、OLE コントロールの**DllInstall**関数を呼び出します。

<a href="" id="timeout"></a>*タイムアウト*  
OLE コントロールが指定された登録解除呼び出しを完了するためのタイムアウト (秒単位) を指定します。 既定のタイムアウトは60秒です。

<a href="" id="argument"></a>*引数*  
コントロールが実行可能ファイルの場合、これは実行可能ファイルに渡されるコマンド文字列です。 既定の引数は **/UnRegServer**です。

コントロールが実行可能ファイルでない場合は、 **DllInstall**関数に渡すコマンドライン引数を指定します。

<a name="remarks"></a>解説
-------

各*登録解除 dll セクション*名は、INF ファイル内で一意である必要があります。また、セクション名を定義するための一般的な規則に従う必要があります。 これらの規則の詳細については、「 [INF ファイルの一般的な構文規則](general-syntax-rules-for-inf-files.md)」を参照してください。

OLE コントロールと自己登録解除の詳細については、Windows SDK のドキュメントを参照してください。

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


[**RegisterDlls**](inf-registerdlls-directive.md)

 

 






