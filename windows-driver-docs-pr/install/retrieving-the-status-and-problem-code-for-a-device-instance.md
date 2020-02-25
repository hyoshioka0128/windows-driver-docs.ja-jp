---
title: デバイス インスタンスの状態と問題コードの取得
description: デバイス インスタンスの状態と問題コードの取得
ms.assetid: 22ca9ac2-fe67-427d-a6e4-f1d9cbbede52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 64149e27e36ac13ef09df63b4545069a39f1865f
ms.sourcegitcommit: aa7083b10b34a29a348f4950ced21a8a67a44a0f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/22/2020
ms.locfileid: "77558405"
---
# <a name="retrieving-the-status-and-problem-code-for-a-device-instance"></a>デバイス インスタンスの状態と問題コードの取得


Windows Vista 以降のバージョンの Windows では、"[デバイスの状態" プロパティと "問題のコード" プロパティ](https://docs.microsoft.com/previous-versions/ff542254(v=vs.85))が[統合デバイスプロパティモデル](unified-device-property-model--windows-vista-and-later-.md)に含まれています。 統合デバイスプロパティモデルは、[プロパティキー](property-keys.md)を使用してこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 は、統合プロパティモデルのプロパティキーをサポートしていません。また、これらのプロパティを表す対応するレジストリエントリの値もサポートしていません。 ただし、対応する情報は、 [**CM_Get_DevNode_Status**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_status)関数を呼び出すことによって取得できます。 以前のバージョンの Windows との互換性を維持するために、Windows Vista 以降のバージョンでも**CM_Get_DevNode_Status**がサポートされています。 ただし、デバイスドライバーのプロパティにアクセスするには、統合されたデバイスプロパティモデルのプロパティキーを使用する必要があります。

デバイスドライバーのプロパティは、Windows Vista 以降のバージョンでプロパティにアクセスするために使用するプロパティキー識別子によって一覧表示されます。

Windows Vista 以降のバージョンで、プロパティキーを使用してデバイスドライバのプロパティにアクセスする方法の詳細については、「デバイスインスタンスのプロパティへのアクセス[(Windows vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)」を参照してください。

Windows Server 2003、Windows XP、および Windows 2000 上のデバイスインスタンスの状態と問題コードにアクセスするには、 **CM_Get_DevNode_Status**を呼び出し、次のパラメーターを指定します。

-   デバイスインスタンスに設定されているステータスビットフラグを受け取る ULONG 型の値への*ポインターに、* 値を指定します。 Status 値には、 *Cfg*に定義されているプレフィックスが "DN_" のビットフラグの任意の組み合わせを指定できます。

-   デバイスインスタンスに設定されている問題の番号を受け取る ULONG 型の値へのポインターに、*値*を設定します。 問題番号は、 *Cfg*に定義されている "CM_PROB_" というプレフィックスを持つ定数の1つです。 **CM_Get_DevNode_Status**は、DN_HAS_PROBLEM が "値を持つ"*状態*に設定されている場合にのみ、問題の番号を設定します。

-   状態と問題コードを取得するデバイスへのデバイスインスタンスハンドルに*Dndevinst*を設定します。

-   *Ulflags*を0に設定します。

**CM_Get_DevNode_Status**の呼び出しが成功した場合、 **CM_Get_DevNode_Status**はデバイスインスタンスの要求された状態と問題コードを取得し、CR_SUCCESS を返します。 関数呼び出しが失敗した場合、 **CM_Get_DevNode_Status**は、 *Cfgmgr32*で定義されているプレフィックスが "CR_" のエラーコードの1つを返します。

## <a name="see-also"></a>参照
 
* [**DEVPKEY_Device_ProblemCode**](devpkey-device-problemcode.md)
* [**DEVPKEY_Device_ProblemStatus**](devpkey-device-problemstatus.md)

