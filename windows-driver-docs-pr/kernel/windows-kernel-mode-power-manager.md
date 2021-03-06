---
title: Windows カーネルモード電源マネージャー
description: Windows カーネルモード電源マネージャー
ms.assetid: 2d39e43a-63a6-4474-a1ed-c24b4526a3f5
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0ed9d501b4c486d8bb482bb8faf704524157d86d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374174"
---
# <a name="windows-kernel-mode-power-manager"></a>Windows カーネルモード電源マネージャー


Windows では、power 管理テクノロジを使用して、電力消費の削減 Pc の一般に、ラップトップのバッテリ電源を具体的には。 たとえば、Windows コンピューターはスリープまたは休止状態に配置できます。 シャット ダウンまたは電力消費の削減に移動するコンピューターの開始時に接続されているデバイスも電源を切断できる適切な方法でデータが失われないようにするために、コンピューターのデバイスの複雑な電源管理システムが進化してきました。 これらのデバイスには、警告が必要がありますを電源の状態を変更するのにも、それらは正しくシャット ダウンするまで待機する制御デバイスに指示する通信ループの一部である必要があるとします。

Windows カーネル モードの電源マネージャーは、電源の状態の変更をサポートするすべてのデバイスの電源の状態で正常に行う変更を管理します。 その他のデバイスを制御するデバイスの複雑なスタックをこれは多くの場合です。 各制御デバイスと呼ばれる、*ノード*デバイス スタックを上下に電源状態の変化の通信を処理できるドライバーが必要とします。

電源状態の変更の影響を受けることがあるドライバーを作成する場合は、次の種類の情報、ドライバーのコードで処理できる必要があります。

-   システム アクティビティのレベル。

-   システムのバッテリ レベル。

-   現在は、シャット ダウン、スリープまたは休止状態を要求します。

-   電源ボタンを押すなどのユーザー アクション。

-   10% のバッテリ電源で自動的にシャット ダウンなどのパネルの設定を制御します。

電源マネージャーは、Irp を使用してこれらの要求を処理します。 Irp の詳細については、次を参照してください。 [Irp の処理](handling-irps.md)します。

電源マネージャーは、電源管理と座標の電源イベントを処理するポリシーの管理と組み合わせて動作し、電源管理 Irp が生成されます。 電源マネージャー、電源の状態を変更する要求を収集します順位のデバイスの電源状態変更、および変更を行う適切なドライバーを通知する適切な Irp を送信し、必要があります (するさらに可能性がありますように指示するサブデバイス、。変わります)。 ポリシー マネージャーは、システムのアクティビティを監視し、電源ポリシーにユーザーの状態、アプリケーションの状態、およびデバイス ドライバ ステータスを統合します。

電源管理に関する情報の詳細を参照してください。[電源管理の Windows ドライバー](implementing-power-management.md)します。

電源マネージャーは、I/O マネージャーのサブコンポーネントと見なされます。 詳細については、次を参照してください。 [Windows I/O マネージャー](windows-kernel-mode-i-o-manager.md)します。

電源マネージャーに直接インターフェイスを提供するルーチンが、通常は付いて"**Po**"。 たとえば、 **PoSetPowerState**します。 電源マネージャー ルーチンの一覧は、次を参照してください。[電源マネージャー ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)します。

Windows Driver Frameworks (WDF) は、電源管理を簡単にライブラリのセットを提供します。 WDF の詳細については、次を参照してください。[カーネル モード ドライバー フレームワークの概要](https://docs.microsoft.com/windows-hardware/drivers/wdf/what-s-new-for-wdf-drivers)します。

 

 




