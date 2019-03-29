---
title: デバイス インスタンスの状態と問題コードの取得
description: デバイス インスタンスの状態と問題コードの取得
ms.assetid: 22ca9ac2-fe67-427d-a6e4-f1d9cbbede52
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc53d29a376517562885c2fb8a13611c812895f5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580640"
---
# <a name="retrieving-the-status-and-problem-code-for-a-device-instance"></a>デバイス インスタンスの状態と問題コードの取得


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)が含まれています、[デバイス状態のプロパティと問題のコード プロパティ](https://msdn.microsoft.com/library/windows/hardware/ff542254)します。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000、統一されたプロパティのモデルのプロパティのキーをサポートしても、これらのプロパティを表す対応するレジストリ エントリの値をサポートしています。 ただし、呼び出すことによって、対応する情報を取得できます、 [ **CM_Get_DevNode_Status** ](https://msdn.microsoft.com/library/windows/hardware/ff538514)関数。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンもサポート**CM_Get_DevNode_Status**します。 ただし、デバイス ドライバーのプロパティにアクセスするのに、統一されたデバイス プロパティのモデルのプロパティのキーを使用する必要があります。

デバイス ドライバーのプロパティは、Windows Vista およびそれ以降のバージョンのプロパティへのアクセスに使用するプロパティのキー識別子が表示されます。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンでデバイス ドライバーのプロパティにアクセスする方法については、次を参照してください。[プロパティへのアクセス デバイス インスタンス (Windows Vista 以降)](accessing-device-instance-properties--windows-vista-and-later-.md)します。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス インスタンスの状態および問題のコードにアクセスするには、呼び出す**CM_Get_DevNode_Status**し、次のパラメーターを指定します。

-   設定*pulStatus*デバイス インスタンスに設定されている状態のビット フラグを受け取る ULONG に型指定された値へのポインター。 状態値は、プレフィックスで定義されている"DN_"で、ビット フラグの任意の組み合わせを指定できます*Cfg.h*します。

-   設定*pulProblemNumber*デバイス インスタンスに設定されている問題の数を受け取る ULONG に型指定された値へのポインター。 問題の数は、プレフィックス"CM_PROB_"で定義されている定数のいずれか*Cfg.h*します。 **CM_Get_DevNode_Status** DN_HAS_PROBLEM 設定されている場合にのみ、問題の数を設定*pulStatus*します。

-   設定*dnDevInst*状態および問題のコードを取得する対象のデバイスへのデバイスのインスタンス ハンドル。

-   設定*ulFlags*をゼロにします。

場合に呼び出し**CM_Get_DevNode_Status**成功すると、 **CM_Get_DevNode_Status**要求された状態とデバイスのインスタンスの問題のコードを取得し、CR_SUCCESS を返します。 関数呼び出しが失敗した場合、 **CM_Get_DevNode_Status**プレフィックスで定義されている"CR_"でエラー コードのいずれかを返します*Cfgmgr32.h*します。

 

 





