---
title: UEFI 環境からデバイス I/O
description: Windows OS ローダー UpdateCapsule 関数を呼び出すと、CapsuleHeaderArray に含まれる各 capsule が実行されます。
ms.assetid: 843B177F-CD1F-47E6-8F35-0A0FFA8FA192
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04ee06201013d4f4874021c3a1211b8586026dc5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558689"
---
# <a name="device-io-from-the-uefi-environment"></a>UEFI 環境からデバイス I/O


Windows OS ローダー UpdateCapsule 関数を呼び出すと、CapsuleHeaderArray に含まれる各 capsule が実行されます。 Capsule の実行順序は、UEFI ファームウェアの実装に依存したり、カプセルことはできませんカプセル他の基準としたことを実行の順序に関して何らかの仮定カプセル他に、依存します。 各 capsule では、UEFI コード、更新プログラムと、ファームウェア イメージを管理する実行可能である両方を構成する、自己完結型ペイロードを示します。

ターミネータが呼び出されたときに、ターゲット デバイスとの通信チャネルを開くため、capsule に含まれる実行可能コードが担当します。 適切なチャネルは、システムのデバイス トポロジでは、対象デバイス、および UEFI ブート サービスと特定の UEFI の実装によって提供されるドライバーの機能によって異なります。 Capsule 実装者は、対象の UEFI 環境で使用できるオプションについては、UEFI BIOS ベンダーに相談する必要があります。 通常、通信は、特定のデバイスの UEFI デバイス ドライバーを利用することで確立されます。 このドライバーは、適切なプロトコルを使用して、よく知られているデバイスのパスを使用してデバイスにバインドする capsule 更新コードになります。

通信が確立されると、更新プログラム管理のコードは、対象となるデバイスにファームウェア イメージを書き込みます。 更新を完了すると、適切な状態の戻り値のコードは、デバイスのファームウェア リソース エントリ、ESRT に書き込まれます。 更新プログラム管理のコードは、コントロールを UpdateCapsule 関数に戻します。

構造、capsule、および UEFI ブート サービス ドライバーと、プロトコルは UpdateCapsule 関数について詳しくを参照してください、 [UEFI 仕様](https://go.microsoft.com/fwlink/p/?LinkId=218221)します。

## <a name="related-topics"></a>関連トピック
[ESRT テーブルの定義](esrt-table-definition.md)  
[プラグ アンド プレイ デバイス](plug-and-play-device.md)  
[更新プログラムのドライバー パッケージの作成](authoring-an-update-driver-package.md)  
[更新プログラムの処理](processing-updates.md)  
[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)  
[ファームウェアの更新状態](firmware-update-status.md)  



