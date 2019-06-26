---
title: ATA コマンドのサポート
description: ATA コマンドのサポート
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f417f9554e0872730dc1c4e4cf52bbf40868ba2f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368410"
---
# <a name="ata-command-support"></a>ATA コマンドのサポート


記憶域デバイスでは、ATA のコマンド セットをサポートする場合 StorPort は ATA のパススルー制御コードを使用してターゲット デバイスに直接 ATA コマンドを送信します。 デバイス管理アプリケーションを使用できる、 [ **IOCTL\_ATA\_渡す\_を通じて**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through)と[ **IOCTL\_ATA\_渡す\_を通じて\_直接**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through_direct)この目的のためのコードを制御します。

このセクションには、特定の ATA コマンド要求を発行するための特別な要件に関する情報が含まれています。

[セキュリティ グループのコマンド](security-group-commands.md)

 

 




