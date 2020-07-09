---
title: HMD と特殊なモニター
description: HMD と特殊なモニター
keywords:
- デバイスの WDK を表示する
- ドライバーの監視 WDK
- ドライバーの表示 WDK、ドライバーの監視
- monitors
- HMD
- 仮想現実
ms.author: windowsdriverdev
ms.date: 11/30/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.localizationpriority: medium
ms.openlocfilehash: 1047f28b1bb6a5924932e5f379acfe3d51470fa0
ms.sourcegitcommit: 8b6d83bcedea8c872ec8c7df874344421a39dd57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/08/2020
ms.locfileid: "86128881"
---
# <a name="hmds-and-specialized-displays"></a>HMDs と特殊化された表示

Windows には、ヘッドマウントされたディスプレイ (HMDs) とその他の種類の "特殊な" 表示シナリオに対するサポートが組み込まれています。 これらの表示は、標準の Windows システムコンポジター (DWM) によって無視されるため、カスタムコンポジターでのみ解決できます。 さらに、HMDs と特殊化された表示には、Windows によって次のプロパティが付与されます。

* システムコンポジター (DWM) によって無視されるため、Windows シェルをこれらの表示に拡張することはできません (壁紙、デスクトップアイコン、タスクバーなど)。
* PC が使用されている間、OS によって自動的に電源がオンになることはありません。
* タッチ入力やマウス入力を受け取ることはありません。
* アクセスモデルに応じて、専用のコントロールとプレゼンテーション用のアプリによってコントロールを取得できます。

Windows Mixed Reality ヘッドセットは、カスタムコンポジターによって制御される HMDs の一例です。 このドキュメントを使用して、サードパーティが同様のソリューションを構築できます。

## <a name="topics"></a>トピック

[HMDs および特殊な表示用の EDID 拡張機能](specialized-monitors-edid-extension.md)

[HMDs および特殊化された表示のためのカスタムコンポジターの構築](specialized-monitors-compositor.md)

## <a name="version-history"></a>バージョン履歴

### <a name="windows-10-version-1709-fall-creators-update"></a>Windows 10 バージョン 1709 (作成者の更新プログラムの分類)

* Windows Mixed Reality には、virtual Reality デバイスのサポートが付属しています。 Windows Mixed Reality デバイスは、HMDs バージョン1用の Microsoft EDID 拡張機能に準拠している必要があります。

### <a name="windows-10-version-1809"></a>Windows 10 バージョン 1809

* Api ファミリを使用してサードパーティの HMD コンポジターを構築するためのサポートを追加しました `Windows.Devices.Display.Core` 。 サポートされているデバイスは、HMDs バージョン2用の Microsoft EDID 拡張機能に準拠している必要があります。

### <a name="windows-10-version-2004"></a>Windows 10 バージョン 2004

* * * Microsoft EDID extension for HMDs および特殊化された表示のバージョン3を含む "特殊化された" ディスプレイのサポートが追加されました。
* * * 設定を使用してモニターを "特殊な" 表示として指定するためのサポートを追加しました。

* * は、Windows 10 Enterprise、Windows 10 Pro (ワークステーション)、Windows 10 IoT Enterprise に適用されます。