---
title: Windows ドライバーの種類
description: Windows ドライバーの種類
ms.assetid: e6696c6b-2d3c-473c-9f46-576fe0c40496
keywords:
- Windows ドライバー WDK、種類
- ドライバー WDK、種類
- カーネル モード ドライバー WDK、種類
- 最上位レベルのドライバー WDK
- 中間ドライバー WDK カーネル
- 最下位レベルのドライバー WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60bd4fc29d5bba51b7dea9966a06cb92d7c116b1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382939"
---
# <a name="types-of-windows-drivers"></a>Windows ドライバーの種類





Microsoft Windows ドライバーの 2 つの基本的な種類あります。

-   *ユーザー モード ドライバー*ユーザー モードで実行し、通常、Win32 アプリケーションとカーネル モード ドライバーまたはその他のオペレーティング システムのコンポーネント間のインターフェイスを提供します。

    たとえば、Windows Vista では、すべてのプリンター ドライバーはユーザー モードで実行します。 プリンター ドライバー コンポーネントの詳細については、次を参照してください。[印刷の概要](https://docs.microsoft.com/windows-hardware/drivers/print/introduction-to-printing)します。

-   *カーネル モード ドライバー* I/O、プラグ アンド プレイのメモリ、プロセスおよびスレッド、セキュリティ、管理とカーネル モードのオペレーティング システムのコンポーネントで構成されると、役員の一部として、カーネル モードで実行します。 カーネル モード ドライバーは、通常重ねられています。 一般より高度なドライバー通常アプリケーションからデータを受信、データをフィルター処理およびデバイスの機能をサポートしている下位レベルのドライバーに渡します。

    一部のカーネル モード ドライバーも*WDM ドライバー*に準拠している、 [Windows Driver Model](windows-driver-model.md) (WDM)。 すべて WDM ドライバーでは、プラグ アンド プレイ、および電源管理をサポートします。 WDM ドライバーがソースと互換性のある (ただし、バイナリ互換性のあるされません) では、Windows 98/Me、Windows 2000 以降のオペレーティング システム。

    オペレーティング システム自体のように、カーネル モード ドライバーを明確に定義された一連の必要な機能を持つ不連続モジュラー コンポーネントとして実装されます。 システム定義のセットを指定するすべてのカーネル モード ドライバー[標準ドライバー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/kernel/introduction-to-standard-driver-routines)します。

次の図は、カーネル モード ドライバーをいくつかの種類に分割します。

![カーネル モード ドライバーの種類を示す図](images/1drvlyrs.png)

ドライバー スタック内のカーネル モード ドライバーの 3 つの基本的な型は、図に示すようにします。 最上位レベル、中級者、および最下位レベル。 各型だけが異なります構造に少しが大幅に機能します。

1.  *最上位レベルのドライバー*します。 最上位レベルのドライバーなど、ファイル システムをサポートするファイル システム ドライバー (fsd に対して表示される) を含めます。

    -   NTFS

    -   ファイル アロケーション テーブル (FAT)

    -   CD-ROM のファイル システム (CDFS)

    最上位レベルのドライバーは、常に、中間レベルの関数および最も低いレベルのハードウェアのバス ドライバーなどの低レベルの基になるドライバーからのサポートに依存します。

2.  *ドライバーの中間*仮想ディスク、ミラー、またはデバイス固有の種類など、*クラス ドライバー*します。 中間ドライバーは、下位レベルの基になるドライバーからのサポートに依存します。 中間ドライバーは、次のように細分化さらに。

    -   [*関数のドライバー* ](function-drivers.md) I/O バス上の特定の周辺機器を制御します。

    -   [*フィルター ドライバー* ](filter-drivers.md)自身関数ドライバーより上または下に挿入します。

    -   *ソフトウェア バス ドライバー*デバイスもより高度なクラス、関数、またはフィルター ドライバーを添付できます自体の子のセットを表示します。

        たとえば、異種デバイスの内蔵型のセットで多機能なアダプターを制御するドライバー ソフトウェア バス ドライバーとは。

    -   いずれかのシステム提供*クラス ドライバー*エクスポート システム定義のクラス/miniclass インターフェイスが、実際には、1 つまたは複数のリンクされた中間のドライバー *miniclass ドライバー* (とも呼ばれる*ミニドライバー*)。 リンクされたクラス/ミニドライバーの各ペアは、関数のドライバーまたはソフトウェア バス ドライバーの相当する機能を提供します。

3.  *最下位レベルのドライバー*周辺機器が接続されている、I/O バスを制御します。 最下位レベルのドライバーは、下位レベルのドライバーに依存しません。

    -   ハードウェア[*バス ドライバー* ](bus-drivers.md)はシステムが提供し、通常は動的に構成可能な I/O バスを制御します。

        ハードウェア バス ドライバーを構成して、ドライバーを制御する I/O バスに接続されているすべての子デバイス用のシステムのハードウェア リソースを再構成するプラグ アンド プレイ manager を使用します。 これらのハードウェア リソースには、デバイス メモリと割り込み要求 (Irq) のためのマッピングが含まれます。 (ハードウェア バス ドライバー包含 HAL コンポーネントは、Windows NT ベース オペレーティング システムを Windows 2000 より前のリリースで提供される機能の一部です。)

    -   *レガシ ドライバー*直接物理デバイスのコントロールが最下位レベルのドライバーです。

 

 




