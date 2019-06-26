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
ms.openlocfilehash: 54583b2ddeaf0dc5df681322853dc86f441e0ea1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384925"
---
# <a name="opening-a-handle-to-a-registry-key-object"></a>レジストリ キー オブジェクトのハンドルを開く





レジストリ キー オブジェクトを識別するハンドルを開くには、次の 2 段階のプロセスを実行します。

1.  作成、 [**オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/ns-wudfwdm-_object_attributes)構造体、およびそれを呼び出すことによって初期化[ **InitializeObjectAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfwdm/nf-wudfwdm-initializeobjectattributes)します。 として操作するキーの名前を指定する、 *ObjectName*パラメーターを**InitializeObjectAttributes**します。

    渡した場合**NULL**として、 *RootDirectory*パラメーターを**InitializeObjectAttributes**、 *ObjectName*の完全なパスを指定する必要があります、以降では、レジストリ キー **\\レジストリ**します。 それ以外の場合、 *RootDirectory*キーへのオープン ハンドルである必要がありますと*ObjectName*はそのキーに対して相対的なパスです。

2.  呼び出すことによって、キー オブジェクトへのハンドルを開く[ **ZwCreateKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)または[ **ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwopenkey)を渡すと、**オブジェクト\_属性**を構造体。 キーが存在しない場合**ZwCreateKey** 、キーが作成されますが、 **ZwOpenKey**ステータスを返します\_オブジェクト\_名前\_いない\_見つかりました。

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

 

使用できる値の詳細については、 *DesiredAccess*パラメーターを参照してください[ **ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-zwcreatekey)します。

呼び出すこともできます[ **IoOpenDeviceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)と[ **IoOpenDeviceInterfaceRegistryKey** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)をこれらのレジストリ キーへのハンドルを開く特定のデバイスと、特定のデバイス インターフェイスをそれぞれです。 詳細については、次を参照してください。[プラグ アンド プレイ レジストリ ルーチン](plug-and-play-registry-routines.md)します。

**注**  への呼び出しに**ZwCreateKey**、 **ZwOpenKey**、 **IoOpenDeviceRegistryKey**、および**IoOpenDeviceInterfaceRegistryKey**、汎用的なアクセス権、ジェネリック\_読み取りとジェネリック\_記述では、キーのキーに固有のアクセス権を意味的に同等です\_読み取りとキー\_書き込み、それぞれ、および、これらのキーに固有のアクセス権の代替として使用できます。

 

 

 




