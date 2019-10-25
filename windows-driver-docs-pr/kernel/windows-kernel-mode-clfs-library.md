---
title: Windows カーネルモード CLFS ライブラリ
description: Windows カーネルモード CLFS ライブラリ
ms.assetid: 4da3cb49-dc20-4713-813b-ff458c99ab90
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b66a01250770cf0f5644d34b7c53a16e031ece16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835733"
---
# <a name="windows-kernel-mode-clfs-library"></a>Windows カーネルモード CLFS ライブラリ


Windows には、システムファイル用のトランザクションログシステムが用意されています。 このシステムは、共通ログファイルシステム (CLFS) と呼ばれます。 CLFS の詳細については、「[共通ログファイルシステム](using-common-log-file-system.md)」を参照してください。

CLFS の直接インターフェイスを提供するルーチンには、"**CLFS**" という文字がプレフィックスとして付けられます。CLFS ライブラリルーチンの一覧については、「[共通ログファイルシステム (CLFS) ライブラリルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。 CLFS には、CLFS を管理するために実装できるルーチンの一覧も用意されています。CLFS management の詳細については、「 [CLFS Management Library ルーチン](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)」を参照してください。

CLFS は、トランザクション処理されたファイルシステムに関連するテクノロジです。トランザクションの詳細については、「 [Windows カーネルモードトランザクションマネージャー](windows-kernel-mode-kernel-transaction-manager.md)」を参照してください。

 

 




