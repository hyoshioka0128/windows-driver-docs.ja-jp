---
title: UEFI 環境からのデバイス I/O
description: Windows OS ローダーが UpdateCapsule 関数を呼び出すと、CapsuleHeaderArray に含まれる各カプセルが実行されます。
ms.assetid: 843B177F-CD1F-47E6-8F35-0A0FFA8FA192
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: 87f54e308f84c6b96fb7b6564ab0197e7da577ba
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769384"
---
# <a name="device-io-from-the-uefi-environment"></a>UEFI 環境からのデバイス I/O

Windows OS ローダーが UpdateCapsule 関数を呼び出すと、CapsuleHeaderArray に含まれる各カプセルが実行されます。 カプセル実行の順序は、UEFI ファームウェアの実装に依存します。また、カプセルは、他の capsules に対して実行の順序を想定したり、他の capsules に依存関係を取得したりすることはできません。 各カプセルは自己完結型のペイロードで、更新プログラムとファームウェアイメージを管理するための実行可能な UEFI コードの両方で構成されています。

カプセルが呼び出されると、カプセルに含まれる実行可能コードは、ターゲットデバイスとの通信チャネルを開く役割を担います。 適切なチャネルは、システムのデバイストポロジ、ターゲットデバイスの機能、および特定の UEFI 実装によって提供される UEFI ブートサービスとドライバーによって異なります。 カプセル化の実装では、対象となる UEFI 環境で利用できるオプションについて、UEFI BIOS ベンダーに問い合わせる必要がある場合があります。 通常、通信は、特定のデバイスに対して UEFI デバイスドライバーを使用することによって確立されます。 このドライバーは、適切なプロトコルを使用して既知のデバイスパス経由でデバイスにバインドするように、カプセル化更新コードを有効にします。

通信が確立されると、更新管理コードは、ターゲットデバイスにファームウェアイメージを書き込みます。 更新が完了すると、適切なリターンステータスコードが ESRT のデバイスのファームウェアリソースエントリに書き込まれます。 更新管理コードは、UpdateCapsule 関数に制御を戻します。

UpdateCapsule 関数、カプセルの構造、および UEFI ブートサービスのドライバーとプロトコルの詳細については、 [uefi 仕様](https://uefi.org/specifications)を参照してください。

## <a name="related-topics"></a>関連トピック

[ESRT テーブルの定義](esrt-table-definition.md)  

[プラグ アンド プレイ デバイス](plug-and-play-device.md)  

[更新プログラム ドライバー パッケージの作成](authoring-an-update-driver-package.md)  

[更新プログラムの処理](processing-updates.md)

[シームレスな危機防止と回復](seamless-crisis-prevention-and-recovery.md)

[ファームウェア更新の状態](firmware-update-status.md)  
