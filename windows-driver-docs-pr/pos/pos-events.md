---
title: POS のイベント
description: Readfile 関数を使用して、デバイス ドライバーから Point of Service (POS) API レイヤーに渡されるイベントについて説明します。
ms.assetid: 1123b789-c0ee-4490-9081-79c08fc31417
ms.date: 09/07/2018
ms.localizationpriority: medium
ms.openlocfilehash: 629658ba43349510468469b837a4d8a4a6d9bf7f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56572410"
---
# <a name="pos-events"></a>POS のイベント

このセクションに渡されるデバイス ドライバから Point of Service (POS) API レイヤーを使用してイベントを説明します[ReadFile](https://docs.microsoft.com/windows/desktop/api/fileapi/nf-fileapi-readfile)します。 アプリケーションは、POS API を使用してデバイスを正常に要求、ときに、ランタイムはイベントを受信するデバイス ドライバーに対して継続的な読み取り操作を維持します。 I/O は、メッセージ ベースです。 **ReadFile**を現在のイベントを読み取るように十分な十分な大きさのバッファーに渡す必要があります。 ドライバーは、全体のメッセージを読み取るための十分な出力バッファーに読み取り要求されるまで、メッセージを保持します。

## <a name="in-this-section"></a>このセクションの内容

[ReleaseDeviceRequested](releasedevicerequested.md)

[StatusUpdated](statusupdated.md)
