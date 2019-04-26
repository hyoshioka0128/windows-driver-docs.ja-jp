---
title: 磁気ストライプ リーダーのイベント
description: Readfile 関数を使用して、デバイス ドライバーから Point of Service (POS) API レイヤーに渡されるイベントについて説明します。
ms.assetid: 48ce9fcb-5ea2-4045-92df-990d94e5e98b
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: b8f45fcc9c7be37d37a14ba84755d3dee8bb82a5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349311"
---
# <a name="magnetic-stripe-reader-events"></a>磁気ストライプ リーダーのイベント

このセクションに渡されるデバイス ドライバから Point of Service (POS) API レイヤーを使用してイベントを説明します[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)します。 このセクションでは、磁気ストライプ リーダー (MSRs) に固有のイベントについて説明します。

## <a name="in-this-section"></a>このセクションの内容

[MagneticStripeReaderDataReceived](magneticstripereaderdatareceived.md)  
スキャンが成功イベントの後に発生します。

[MagneticStripeReaderErrorOccured](magneticstripereadererroroccured.md)  
スキャンのエラーなど、MSR エラーがあるときに発生します。
