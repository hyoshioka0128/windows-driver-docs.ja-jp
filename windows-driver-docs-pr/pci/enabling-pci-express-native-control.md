---
title: Windows での PCI Express ネイティブ コントロールの有効化
description: Windows の PCI Express のネイティブ コントロールの機能によって制御できる、PCI Express 機能
ms:assetid: 0E3A4408-CBF7-494F-9F25-7C78E04526B4
keywords: ACPI、ACPI \_OSC メソッド
ms.date: 06/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7b6d3572482779b7b0db40bd1e6936fb59034a88
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379760"
---
# <a name="enabling-pci-express-native-control-in-windows"></a>Windows での PCI Express ネイティブ コントロールの有効化

Advanced Configuration and Power Interface (ACPI) オペレーティング システムの機能 (\_OSC) 機能の中の通信にメソッドを使用またはオペレーティング システムでは、プラットフォームで利用できる機能を制御できます。 このメソッドは、バージョン 4.0 は、ACPI 仕様で定義されます。

次の表では、Windows Vista、Windows Server 2008 および Windows の以降のバージョンの PCI Express のネイティブ コントロールの機能によって制御できる PCI Express 機能を示します。 これらの機能が、PCI Express の技術仕様で定義されて、ACPI を介してオペレーティング システムによって制御されます\_OSC メソッド。

| PCI Express 機能                        | PCI Express ネイティブ コントロール |
| ------------------------------------------ | -------------------------- |
| PCI Express ネイティブのホット プラグ                | 必須                  |
| PCI Express ネイティブの電源管理イベント | 必須                  |
| PCI Express 詳細エラー報告       | 省略可能                   |
| PCI Express 機能の構造の制御   | 必須                  |

場合、 \_OSC メソッドは、PCI Express のネイティブ コントロールの機能により、Windows オペレーティング システムでは、これらの機能の制御を与えます。 PCI Express のネイティブ コントロール機能は、Windows は依存の PCI Express Advanced エラー報告 (AER)、あり、そのため、PCI Express AER のプラットフォームのサポートは省略可能です。

プラットフォームが実装していない場合、 \_OSC メソッド、または、 \_OSC メソッドは、通信したがっては付与されません、必須のコントロールを表に示す PCI Express 機能のいずれかのオペレーティング システムのコントロールは使用できませんオペレーティング システムに上記の機能、し、Windows が有効になりません PCI Express のネイティブ コントロールでの高度な PCI Express 機能のいずれか。

詳細については、「6.2.10 PCI ファームウェア仕様セクション 4.5 の ACPI 仕様、およびリビジョン 4.0 で、を参照してください。

これらの仕様は、ACPI と PCI SIG Web サイトで使用できます。

  - [ACPI の web サイト](https://www.uefi.org/specifications)
  - [PCI SIG の web サイト](http://www.pcisig.org/)

## <a name="see-also"></a>関連項目
[デバイス固有のデータ (_DSD) PCIe ルート ポート](dsd-for-pcie-root-ports.md)
