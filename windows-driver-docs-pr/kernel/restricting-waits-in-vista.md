---
title: Vista での待機の制限
description: Vista での待機の制限
ms.assetid: edcc25d0-bcf6-48f0-832e-3f911bd42142
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c85817e95bfe65093f1ad221bcdb531f8f4f630c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324359"
---
# <a name="restricting-waits-in-vista"></a>Vista での待機の制限


多くのデバイス ドライバー開発者が使用するため[同期 I/O のプログラミング手法](synchronous-i-o-programming.md)Windows は速度が低下したり、""中にフリーズをデバイスには、応答時間がかかっています。 この問題を減らすためには、Vista の I/O マネージャーには「スタック」デバイスしばらく後に応答を待機しているプログラムの実行は停止します。

**注**  強くお勧めする[同期 I/O のプログラミング手法](synchronous-i-o-programming.md)デバイス ドライバーは回避されます。 Vista は、デバイスのドライバーが待機しているため、ドライバー コードの実行を停止する場合、デバイスが不明な状態で残る可能性が。

 

 

 




