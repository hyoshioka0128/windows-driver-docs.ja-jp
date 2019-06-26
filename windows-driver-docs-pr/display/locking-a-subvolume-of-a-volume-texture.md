---
title: ボリューム テクスチャのサブボリュームのロック
description: ボリューム テクスチャのサブボリュームのロック
ms.assetid: fff7b9c6-5f83-4691-9e44-99e45897ae3a
keywords:
- WDK DirectX 8.0 のテクスチャ
- Windows 2000 の WDK の表示、ボリュームのテクスチャの DirectX 8.0 リリース ノートします。
- ボリューム テクスチャ WDK DirectX 8.0
- subvolume WDK DirectX 8.0 のロック
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d8f79b87df37573d47ec63d4f8b246b6f7f9911
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360900"
---
# <a name="locking-a-subvolume-of-a-volume-texture"></a>ボリューム テクスチャのサブボリュームのロック


## <span id="ddk_locking_a_subvolume_of_a_volume_texture_gg"></span><span id="DDK_LOCKING_A_SUBVOLUME_OF_A_VOLUME_TEXTURE_GG"></span>


DirectX 8.1 にはボリューム テクスチャの subvolume だけをロックするドライバーをできる新しい機能が導入されています。 ときに、ドライバーの[ *DdLock* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_lock)関数が呼び出されると、ドライバーは、ボリューム全体のテクスチャではなく subvolume だけをロックすることによりシステム パフォーマンスを向上させることができます。

この機能のサポートを示すために、ドライバーは、D3DDEVCAPS を設定する必要があります\_SUBVOLUMELOCK ビット、 **DevCaps** D3DCAPS8 構造体のメンバー。 ドライバーがへの応答で D3DCAPS8 構造体を返します、 **GetDriverInfo2** 」の説明に従ってクエリ[DirectX 8.0 スタイル Direct3D の機能を Reporting](reporting-directx-8-0-style-direct3d-capabilities.md)します。 このクエリのサポートについては、「[サポート GetDriverInfo2](supporting-getdriverinfo2.md)します。

この機能のサポートが確認された後、ドライバーを受信できます、 *DdLock*呼び出しが、DDLOCK\_HASVOLUMETEXTUREBOXRECT ビットが設定で、 **dwFlags**渡された DDのメンバー\_LOCKDATA 構造体。 このビットは、指定した subvolume テクスチャをロックダウンするドライバーを通知します。 ドライバーはからロックされた subvolume のフロント エンドとバックエンドの座標を取得する必要がありますし、**左**と**右**で指定されている RECTL 構造体のメンバー、 **rArea**DD のメンバー\_LOCKDATA します。 ドライバーの上位 16 ビットからフロント エンドとバックエンドの座標を取得する、**左**と**右**メンバーそれぞれします。

ロックされた subvolume の左と右の座標は、の下位 16 ビットに制限されます、**左**と**右**メンバー。 ドライバーを使用して、**上部**と**下部**、RECTL のメンバーが構造体**rArea**ロック subvolume の上端と下端の座標を指定する変更されません。 この方法で、 **rArea**メンバーが効果的にロックされている subvolume を指定する 3 つの座標セットを提供します。 RECTL 構造体は、Microsoft Windows SDK ドキュメントで説明します。

次のコードでは、前面の取得し、座標をバックアップする方法を示します。

```cpp
"real" left = rArea.left && 0xFFFF;
"real" right = rArea.right && 0xFFFF;
front = rArea.left >> 16;
back = rArea.right >> 16;
```

この機能は、Windows Me、Windows XP およびそれ以降のバージョンで使用できます。 この機能も Windows 2000 および Windows 98 オペレーティング システムのバージョンにインストールされている DirectX 8.1 ランタイムがあるに使用できます。

 

 





