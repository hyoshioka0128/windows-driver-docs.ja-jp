---
title: レジストリ キー オブジェクトのハンドルを開く
description: レジストリ キー オブジェクトのハンドルを開く
ms.assetid: 451e36a1-1cc2-469e-9f54-c02fef7b1666
keywords:
- レジストリ WDK カーネルでは、オブジェクトのルーチン
- ドライバーのレジストリ情報 WDK カーネル、オブジェクトのルーチン
- オブジェクトのルーチンの WDK カーネル
- レジストリ キー オブジェクトの WDK カーネル
- レジストリ キー オブジェクトへのハンドルを開く
- WDK カーネルのレジストリ キー オブジェクトへのハンドルします。
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41051871ed71f806dd6d8f6c8727a19759b97871
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352063"
---
# <a name="opening-a-handle-to-a-registry-key-object"></a>レジストリ キー オブジェクトのハンドルを開く





レジストリ キー オブジェクトを識別するハンドルを開くには、次の 2 段階のプロセスを実行します。

1.  作成、 [**オブジェクト\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)構造体、およびそれを呼び出すことによって初期化[ **InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804)します。 として操作するキーの名前を指定する、 *ObjectName*パラメーターを**InitializeObjectAttributes**します。

    渡した場合**NULL**として、 *RootDirectory*パラメーターを**InitializeObjectAttributes**、 *ObjectName*の完全なパスを指定する必要があります、以降では、レジストリ キー **\\レジストリ**します。 それ以外の場合、 *RootDirectory*キーへのオープン ハンドルである必要がありますと*ObjectName*はそのキーに対して相対的なパスです。

2.  呼び出すことによって、キー オブジェクトへのハンドルを開く[ **ZwCreateKey** ](https://msdn.microsoft.com/library/windows/hardware/ff566425)または[ **ZwOpenKey**](https://msdn.microsoft.com/library/windows/hardware/ff567014)を渡すと、**オブジェクト\_属性**を構造体。 キーが存在しない場合**ZwCreateKey** 、キーが作成されますが、 **ZwOpenKey**ステータスを返します\_オブジェクト\_名前\_いない\_見つかりました。

渡す、 *DesiredAccess*パラメーターを**ZwCreateKey**または**ZwOpenKey**を要求するアクセス権を格納しています。 ドライバー、操作を許可するアクセス権が実行を指定する必要があります。 次の表は、実行できる操作と要求に対応するアクセス権を示します。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>操作</th>
<th>必要なアクセス権</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>レジストリ キー値を取得します。</p></td>
<td><p>KEY_QUERY_VALUE または KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>レジストリ キー値を設定します。</p></td>
<td><p>KEY_SET_VALUE または KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>すべてのキーのサブキーをループします。</p></td>
<td><p>KEY_ENUMERATE_SUB_KEYS または KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>サブキーを作成します。</p></td>
<td><p>KEY_CREATE_SUB_KEY または KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>キーを削除します。</p></td>
<td><p>DELETE</p></td>
</tr>
</tbody>
</table>

 

使用できる値の詳細については、 *DesiredAccess*パラメーターを参照してください[ **ZwCreateKey**](https://msdn.microsoft.com/library/windows/hardware/ff566425)します。

呼び出すこともできます[ **IoOpenDeviceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549443)と[ **IoOpenDeviceInterfaceRegistryKey** ](https://msdn.microsoft.com/library/windows/hardware/ff549433)をこれらのレジストリ キーへのハンドルを開く特定のデバイスと、特定のデバイス インターフェイスをそれぞれです。 詳細については、次を参照してください。[プラグ アンド プレイ レジストリ ルーチン](plug-and-play-registry-routines.md)します。

**注**  への呼び出しに**ZwCreateKey**、 **ZwOpenKey**、 **IoOpenDeviceRegistryKey**、および**IoOpenDeviceInterfaceRegistryKey**、汎用的なアクセス権、ジェネリック\_読み取りとジェネリック\_記述では、キーのキーに固有のアクセス権を意味的に同等です\_読み取りとキー\_書き込み、それぞれ、および、これらのキーに固有のアクセス権の代替として使用できます。

 

 

 




