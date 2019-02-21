---
Description: Guidance for the Hardware Vendor
title: ハードウェア ベンダーのガイダンス
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56f5dddc0b11c2139c132d0ac410d11b980c2316
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56535934"
---
# <a name="guidance-for-the-hardware-vendor"></a>ハードウェア ベンダーのガイダンス


ポータブル デバイスを製造し、Windows との接続を必要とすると場合、は、次のオプションがあります。

-   クラス以外のプロトコルでデバイスの場合は、WPD ドライバーを提供します。 たとえば、デバイスは、コンピューターとの通信に RS232 経由でのカスタム プロトコルを使用する場合 WPD アプリケーションがデバイスにアクセスできるように WPD ドライバーを提供する必要があります。
-   ポータブル ミュージック プレーヤー デバイスでは、デバイスに MTP などのプロトコルをクラスを実装します。 これは、(Microsoft では、1 つ提供します) ために、ドライバーを指定する必要はありません、WPD と互換性があるデバイスを有効になります。
-   デジタルの静止カメラ PTP/MTP などのクラスのプロトコルを実装します。 MTP では、拡張機能には、PTP よりで最適な選択肢であるため。 ただし、互換性の理由からは、MTP 実装に PTP との下位互換性があることをお勧めします。
-   携帯電話やその他の多機能デバイスでは、デバイスの MTP などのクラス プロトコルを実装します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





