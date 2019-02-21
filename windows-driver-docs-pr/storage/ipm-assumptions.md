---
title: IPM の前提条件
description: IPM の前提条件
ms.assetid: 3c8d8121-9987-43d3-b573-4ca1d26fef7d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c99cb643e669012413b4800d423a923cc4588377
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56552766"
---
# <a name="ipm-assumptions"></a>IPM の前提条件


LUN に SCSI 開始ユニット コマンドの発行時から 240 秒 (4 分) 以内、ディスクをスピン アップする操作を完了します。

次の SCSI コマンド (SRB\_関数\_EXECUTE\_SCSI 操作)、ディスクをスピンアップせずに完了する必要があります。 つまり、前の開始単体の SCSI コマンドを必要はありません。

照会

レポートの LUN

ミニポート ドライバーが SRB を除くすべてされる Srb の完了に予想される\_関数\_IO\_コントロール、SRB\_関数\_のフラッシュと SRB\_関数\_LUN がシャット ダウン省電力状態。

 

 




