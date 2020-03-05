---
title: デバイス インスタンスの状態と問題コードの取得
description: デバイス インスタンスの状態と問題コードの取得
ms.assetid: 22ca9ac2-fe67-427d-a6e4-f1d9cbbede52
ms.date: 02/28/2020
ms.localizationpriority: medium
ms.openlocfilehash: 4bf288c1068969048b7da09aadc8998855d7c4a2
ms.sourcegitcommit: 6f165a03303b7e4950b37d4b992f0f481b14f3ca
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2020
ms.locfileid: "78279451"
---
# <a name="retrieving-the-status-and-problem-code-for-a-device-instance"></a>デバイス インスタンスの状態と問題コードの取得


Windows Vista 以降のバージョンの Windows では、"デバイスの状態" プロパティと "問題のコード" プロパティが[統合デバイスプロパティモデル](unified-device-property-model--windows-vista-and-later-.md)に含まれています。 統合デバイスプロパティモデルは、[プロパティキー](property-keys.md)を使用してこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 は、統合プロパティモデルのプロパティキーをサポートしていません。また、これらのプロパティを表す対応するレジストリエントリの値もサポートしていません。 ただし、対応する情報は、 [**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)関数を呼び出すことによって取得できます。 以前のバージョンの Windows との互換性を維持するために、Windows Vista 以降のバージョンでも**CM_Get_DevNode_Status**がサポートされています。 ただし、デバイスドライバーのプロパティにアクセスするには、統合されたデバイスプロパティモデルのプロパティキーを使用する必要があります。

デバイスドライバーのプロパティは、Windows Vista 以降のバージョンでプロパティにアクセスするために使用するプロパティキー識別子によって一覧表示されます。

Windows Vista 以降のバージョンで、プロパティキーを使用してデバイスドライバのプロパティにアクセスする方法の詳細については、「デバイスインスタンスのプロパティへのアクセス[(Windows vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)」を参照してください。

Windows Server 2003、Windows XP、および Windows 2000 上のデバイスインスタンスの状態と問題コードにアクセスするには、 **CM_Get_DevNode_Status**を呼び出し、次のパラメーターを指定します。

-   デバイスインスタンスに設定されているステータスビットフラグを受け取る ULONG 型の値への*ポインターに、* 値を指定します。 Status 値には、 *Cfg*に定義されているプレフィックスが "DN_" のビットフラグの任意の組み合わせを指定できます。

-   デバイスインスタンスに設定されている問題の番号を受け取る ULONG 型の値へのポインターに、*値*を設定します。 問題番号は、 *Cfg*に定義されている "CM_PROB_" というプレフィックスを持つ定数の1つです。 **CM_Get_DevNode_Status**は、DN_HAS_PROBLEM が "値を持つ"*状態*に設定されている場合にのみ、問題の番号を設定します。

-   状態と問題コードを取得するデバイスへのデバイスインスタンスハンドルに*Dndevinst*を設定します。

-   *Ulflags*を0に設定します。

**CM_Get_DevNode_Status**の呼び出しが成功した場合、 **CM_Get_DevNode_Status**はデバイスインスタンスの要求された状態と問題コードを取得し、CR_SUCCESS を返します。 関数呼び出しが失敗した場合、 **CM_Get_DevNode_Status**は、 *Cfgmgr32*で定義されているプレフィックスが "CR_" のエラーコードの1つを返します。

## <a name="using-device-manager-to-find-problem-code-and-problem-status-for-a-device"></a>デバイスマネージャーを使用したデバイスの問題コードと問題の状態の検出

Devnode に問題があると、 **[デバイスの状態]** フィールドの **[全般]** タブに問題コードが表示されます。

**問題の状態**プロパティは、デバイスマネージャーのデバイスの **[詳細]** タブの**プロパティ**のドロップダウンに表示されます。

## <a name="using-the-debugger-to-find-problem-code-and-problem-status-for-a-device"></a>デバッガーを使用してデバイスの問題コードと問題の状態を検出する

カーネルデバッガーに問題コードがあるすべてのデバイスを表示するには、 [ **! devnode 0 21**](../debugger/-devnode.md)拡張機能を使用します。 これにより、デバイスの状態も表示されます。 例 :

```
0: kd> !devnode 0 21
Dumping IopRootDeviceNode (= 0x85d37e30)
DevNode 0x8ad6ab78 for PDO 0x81635c30
  InstancePath is "ROOT\DIINSTALLDRIVER\0003"
  ServiceName is "isolated"
  State = DeviceNodeRemoved (0x312)
  Previous State = DeviceNodeInitialized (0x302)
  Problem = CM_PROB_FAILED_ADD
  Problem Status = 0xc00000bb
```

**[! Devnode]** (. を発行して、問題のコードと問題の状態を表示することもできます。/debugger/-devnode.md) DEVICE_NODE のアドレス:

```
0: kd> !devnode 0x8ad6ab78 
DevNode 0x8ad6ab78 for PDO 0x81635c30
  Parent 0x85d37e30   Sibling 0x8adee670   Child 0000000000   
  ...
  Problem = CM_PROB_FAILED_ADD
  Problem Status = 0xc00000bb
```

この情報は、デバイスマネージャーの実行中のシステムにも表示されます。 詳細については、「 [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)」を参照してください。

## <a name="see-also"></a>参照
 
* [**DEVPKEY_Device_ProblemCode**](devpkey-device-problemcode.md)
* [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

