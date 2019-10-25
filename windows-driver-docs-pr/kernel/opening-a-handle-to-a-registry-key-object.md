---
title: レジストリキーオブジェクトへのハンドルを開く
description: レジストリキーオブジェクトへのハンドルを開く
ms.assetid: 451e36a1-1cc2-469e-9f54-c02fef7b1666
keywords:
- レジストリ WDK カーネル、オブジェクトルーチン
- ドライバーレジストリ情報 WDK カーネル、オブジェクトルーチン
- オブジェクトルーチン WDK カーネル
- レジストリキーオブジェクト WDK カーネル
- レジストリキーオブジェクトへのハンドルを開いています
- レジストリキーオブジェクト WDK カーネルに対するハンドル
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a33e5440c2a723eef1f600e21958587fdf09a1b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838526"
---
# <a name="opening-a-handle-to-a-registry-key-object"></a>レジストリキーオブジェクトへのハンドルを開く





レジストリキーオブジェクトへのハンドルを開くには、次の2段階のプロセスを実行します。

1.  [**オブジェクト\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/ns-wudfwdm-_object_attributes)構造体を作成し、 [**initializeobjectattributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfwdm/nf-wudfwdm-initializeobjectattributes)を呼び出して初期化します。 を操作するキーの名前を、 **Initializeobjectattributes**に対する*ObjectName*パラメーターとして指定します。

    *Rootdirectory*パラメーターとして**Initializeobjectattributes**に**NULL**を渡す場合、 *ObjectName*には **\\registry**で始まるレジストリキーの完全なパスを指定する必要があります。 それ以外の場合、 *Rootdirectory*はキーを開くハンドルである必要があります。 *ObjectName*は、そのキーに対する相対パスです。

2.  [**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)または[**zwopenkey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)を呼び出してキーオブジェクトへのハンドルを開き、**オブジェクト\_属性**構造体に渡します。 キーがまだ存在しない場合は、 **ZwCreateKey**によってキーが作成されますが、 **Zwopenkey**は\_オブジェクト\_名\_返され\_見つかりませんでした。

要求するアクセス権を含む**ZwCreateKey**または**Zwopenkey**に*DesiredAccess*パラメーターを渡します。 ドライバーが実行する操作を許可するアクセス権を指定する必要があります。 次の表に、実行できる操作と、要求するためのアクセス権を示します。

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
<td><p>レジストリキー値を取得します。</p></td>
<td><p>KEY_QUERY_VALUE または KEY_READ</p></td>
</tr>
<tr class="even">
<td><p>レジストリキーの値を設定します。</p></td>
<td><p>KEY_SET_VALUE または KEY_WRITE</p></td>
</tr>
<tr class="odd">
<td><p>キーのすべてのサブキーをループします。</p></td>
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

 

*DesiredAccess*パラメーターで使用できる値の詳細については、「 [**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)」を参照してください。

また、 [**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)と[**IoOpenDeviceInterfaceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)を呼び出して、それぞれがデバイス固有のレジストリキーおよびデバイスインターフェイスに固有のハンドルを開くこともできます。 詳細については、「[プラグアンドプレイ Registry ルーチン](plug-and-play-registry-routines.md)」を参照してください。

**ZwCreateKey**、 **zwopenkey**、 **IoOpenDeviceRegistryKey**、および**IoOpenDeviceInterfaceRegistryKey**の呼び出しでは、汎用アクセス権、一般\_読み取りと汎用\_書き込みは **、  ** キー固有のアクセス権、キー\_読み取りとキー\_書き込みの意味では、これらのキー固有のアクセス権の代替として使用できます。

 

 

 




