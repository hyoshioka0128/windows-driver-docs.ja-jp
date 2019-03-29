---
title: ATA コマンドのサポート
description: ATA コマンドのサポート
ms.assetid: 98149A59-3435-4166-8250-EEFBA44DFD4C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6cdf12efd15059012e3bd4019c3a82f9c2b0bfbe
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56574504"
---
# <a name="ata-command-support"></a>ATA コマンドのサポート


記憶域デバイスでは、ATA のコマンド セットをサポートする場合 StorPort は ATA のパススルー制御コードを使用してターゲット デバイスに直接 ATA コマンドを送信します。 デバイス管理アプリケーションを使用できる、 [ **IOCTL\_ATA\_渡す\_を通じて**](https://msdn.microsoft.com/library/windows/hardware/ff559309)と[ **IOCTL\_ATA\_渡す\_を通じて\_直接**](https://msdn.microsoft.com/library/windows/hardware/ff559315)この目的のためのコードを制御します。

このセクションには、特定の ATA コマンド要求を発行するための特別な要件に関する情報が含まれています。

[セキュリティ グループのコマンド](security-group-commands.md)

 

 




