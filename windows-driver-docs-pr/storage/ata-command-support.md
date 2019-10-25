---
title: ATA コマンドのサポート
description: ATA コマンドのサポート
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db69a825af9f88de9fc29876061db43dfeaf012b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72845107"
---
# <a name="ata-command-support"></a>ATA コマンドのサポート


記憶域デバイスが ATA コマンドセットをサポートしている場合、StorPort は ata パススルー制御コードを使用して、ATA コマンドをターゲットデバイスに直接送信します。 デバイス管理アプリケーションでは、この目的のために\_のダイレクト制御コードを使用して\_と[**ioctl\_ata\_渡す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through_direct)ことによっ[**て、ioctl\_ata\_渡す**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddscsi/ni-ntddscsi-ioctl_ata_pass_through)ことができます。

ここでは、特定の ATA コマンド要求を発行するための特別な要件について説明します。

[セキュリティグループのコマンド](security-group-commands.md)

 

 




