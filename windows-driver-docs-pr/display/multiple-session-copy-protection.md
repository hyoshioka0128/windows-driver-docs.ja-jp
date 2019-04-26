---
title: 複数セッションのコピー防止
description: 複数セッションのコピー防止
ms.assetid: f6ac9854-3326-48da-9153-1eec596a157b
keywords:
- 保護 WDK ビデオのミニポート複数セッションをコピーします。
- 複数のセッションのコピー保護 WDK ビデオのミニポート
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1c35ad31da613268a8b9a77de6ef7d01dbd5e22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345584"
---
# <a name="multiple-session-copy-protection"></a>複数セッションのコピー防止


## <span id="ddk_multiple_session_copy_protection_gg"></span><span id="DDK_MULTIPLE_SESSION_COPY_PROTECTION_GG"></span>


コピー保護になっているデバイスのミニポート ドライバーでは、複数の同時コピー防止セッション オプションでサポートできます。 そのために、ミニポート ドライバーは、次を行う必要があります。

-   内の一意のコピー保護キーを返す**dwCPKey**の各コピー保護のアクティブ化します。

-   コピー防止のすべてのセッションは一時的にオフになっているまで有効になっている保持 (担当副社長を通じて\_CP\_CMD\_変更) または非アクティブ化 (担当副社長\_CP\_CMD\_非アクティブ化) します。 たとえば、ミニポート ドライバーを増分またはコピー保護がアクティブになるたびに、参照カウントをデクリメントでした (担当副社長\_CP\_CMD\_アクティブ化) または非アクティブ化/無効、コピー防止を無効にする場合にのみ完全参照カウントには 0 です。

 

 





