---
title: SPCRP_Xxx プロパティの設定
description: SPCRP_Xxx プロパティの設定
ms.assetid: efb0d02e-ec4c-4c1b-900b-c81f504d2919
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e587c8cfbcbd176c17528d2c9f2b6f236f970c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56581211"
---
# <a name="setting-spcrpxxx-properties"></a>SPCRP_Xxx プロパティの設定


Windows Vista および Windows での以降のバージョンで、[統一されたデバイス プロパティのモデル](unified-device-property-model--windows-vista-and-later-.md)サポート、[デバイス セットアップ クラスのプロパティ](https://msdn.microsoft.com/library/windows/hardware/ff542239)で定義されているSPCRP_Xxx識別子に対応しています*Setupapi.h*します。 これらのプロパティには、デバイス セットアップ クラスが特徴付けられます。 統一されたデバイス プロパティのモデルを使用して[プロパティ キー](property-keys.md)をこれらのプロパティを表します。

Windows Server 2003、Windows XP、および Windows 2000 もこれらのデバイス セットアップ クラスのプロパティのほとんどをサポートします。 ただし、Windows の以前のバージョンには、統一されたデバイス プロパティのモデルのプロパティのキーはできません。 代わりに、これらのバージョンの Windows を使用して、SPCRP_*Xxx*デバイスを表す識別子クラスのプロパティを設定します。 Windows の以前のバージョンとの互換性を維持するために Windows Vista およびそれ以降のバージョンも使用をサポートして SPCRP_*Xxx*デバイスのセットアップへのアクセスに識別子クラスのプロパティ。 ただし、デバイス セットアップ クラスのプロパティにアクセスするのに、統一されたデバイス プロパティのモデルのプロパティのキーを使用する必要があります。

システム定義のデバイス セットアップ クラスのプロパティの一覧は、[デバイス セットアップ クラスのプロパティに対応している SPCRP_Xxx 識別子](https://msdn.microsoft.com/library/windows/hardware/ff542245)を参照してください。 デバイス セットアップ クラスのプロパティは、Windows Vista およびそれ以降のバージョンのプロパティへのアクセスに使用するプロパティのキー識別子が表示されます。 プロパティのキーで提供される情報は、対応する SPCRP_ も含まれています。*Xxx*プロパティを、Windows Server 2003、Windows XP、および Windows 2000 へのアクセスに使用できる識別子。

プロパティのキーを使用して、Windows Vista およびそれ以降のバージョンのデバイス セットアップ クラスのプロパティにアクセスする方法については、[にアクセスするデバイス クラスのプロパティ (Windows Vista 以降)](accessing-device-class-properties--windows-vista-and-later-.md)を参照してください。

Windows Server 2003、Windows XP、および Windows 2000 でのデバイス セットアップ クラスのプロパティを設定するには、呼び出す[ **SetupDiSetClassRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552135)し、次のパラメーター値を指定します。

-   設定*ClassGuid*プロパティを設定する対象のデバイス セットアップ クラスを表す GUID へのポインター。

-   設定*プロパティ*にプレフィックス"SPCRP_"に設定するプロパティの識別子。

-   設定*PropertyBuffer*プロパティの値を格納しているバッファーへのポインター。

-   設定*PropertyBufferSize*サイズ (バイト単位) の正しくデータ。

-   設定*MachineName*コンピューター名にします。

-   設定*予約*に**NULL**します。

この呼び出し場合[ **SetupDiSetClassRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff552135)成功すると、 **SetupDiSetClassRegistryProperty**デバイス セットアップ クラスのプロパティを設定し、返します**TRUE**します。 関数呼び出しが失敗した場合、 **SetupDiSetClassRegistryProperty**戻ります**FALSE**への呼び出しと[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)最近記録されたエラー コードを最大限に戻ります。

 

 





