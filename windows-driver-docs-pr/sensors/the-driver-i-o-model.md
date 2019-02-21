---
title: I/O ドライバー モデル
description: ドライバーのサンプルと、加速度計は、シンプルな周辺機器バス、システムの GPIO ピン、およびリソース ハブ経由で通信します。
ms.assetid: 69368837-0599-497F-883C-608DFE014C7E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e8e2498ca01c37a773782b4b74af4f3ca554cfd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535647"
---
# <a name="the-driver-io-model"></a>I/O ドライバー モデル


ドライバーのサンプルと、加速度計は、シンプルな周辺機器バス、システムの GPIO ピン、およびリソース ハブ経由で通信します。

次の図で実行されるコンポーネントの構成を示しています。 ユーザー モード、カーネル モード、および実際のハードウェア。

![io のダイアグラム](images/io.png)

## <a name="simple-peripheral-bus-spb"></a>SPB (Simple Peripheral Bus)


Windows 8.1 では、開発および SPB コント ローラーのドライバーの実装を簡素化するクラス拡張の形式で、SPB コンポーネントをサポートしています。 一般的に、コンポーネントは、次は。

-   登録設定の取得などのリソース ハブでのすべての通信を処理します。
-   同時のターゲットとバスのロック要求を管理する implements 階層化キューの構造体
-   ユーザー モードからカーネル モードのバッファーを変換します。

## <a name="general-purpose-inputoutput-gpio"></a>汎用入力/出力 (GPIO)


Windows 8.1 では、カーネル モード SPB のコンポーネントと同じレベルに配置されている、GPIO のクラスの拡張機能をサポートします。 GPIO クラスの拡張機能は、ドライバーのクライアントの標準的なインターフェイスを提供しつつ、基になるハードウェアの接続と GPIO の場所で柔軟性が向上できます。

SoC の GPIO ピンのプラットフォームは、チップに分散だけでなく SPI に接続されたモデムのようなその他のコンポーネントで公開されています。

## <a name="resource-hub"></a>リソース ハブ


Windows 8.1 には、すべてのデバイスとコント ローラー間の接続を管理するためのリソース ハブがサポートしています。 ハブの保証、必要な開始時刻と停止順序は維持されます。

ハブは、SoC プラットフォームとそのフラット デバイス ツリーにある目的に特化したコンポーネントです。 これらのシステム バスは、次の方法で、Pc と異なります。

-   接続が通常検出不可能です;ACPI で静的に定義されています。
-   ハードウェア コンポーネントに多くの場合、厳密な親子のリレーションシップで複数バスではなくにまたがる複数の依存関係があります。

## <a name="related-topics"></a>関連トピック
[SpbAccelerometer ドライバーのサンプル](spbaccelerometer-driver-sample.md)  
[センサー クラスの拡張機能の使用](using-the-sensor-class-extension.md)  



