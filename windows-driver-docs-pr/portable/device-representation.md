---
Description: Device Representation
title: デバイスの表現
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72998e3834958bd22a71ab287fd549ee3808a930
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56580442"
---
# <a name="device-representation"></a>デバイスの表現


デバイスがある 2 つの主な動作は WPD アーキテクチャによってアドレス指定します。

-   アクセスして、コンテンツを保存します。 たとえば、アプリケーションは、ポータブル ミュージック プレーヤーに音楽ファイルを追加できる必要があります。
-   デバイスをプログラミングします。 これには、設定を変更して、データのキャプチャ、またはファームウェアをアップロードするなどのより複雑な操作のデバイスの準備などの単純な操作が含まれます。 たとえば、**画像の撮影**コマンドを発行して、デジタル カメラする可能性があります。

WPD では、これらの動作は、デバイスを表すオブジェクトの階層として記述されます。 次の図は、多機能デバイスは、この場合、携帯電話 WPD オブジェクト表現を示します。

![wpd 階層](images/wpd_overview_figure3.png)

この階層は、次の機能と内容を示しています。

## <a name="span-idfunctionalityspanspan-idfunctionalityspanspan-idfunctionalityspanfunctionality"></a><span id="Functionality"></span><span id="functionality"></span><span id="FUNCTIONALITY"></span>機能


-   ストレージ オブジェクト。 このデバイスでは、データ ストレージがあります。
-   サービスを接続します。 このサービスは、関数型のオブジェクトを同期し、電話に連絡先を格納するために使用できます。
-   SMS サービス。 このサービスは、送信、受信、および SMS メッセージの格納に使用できる機能のオブジェクトです。

## <a name="span-idcontentsspanspan-idcontentsspanspan-idcontentsspancontents"></a><span id="Contents"></span><span id="contents"></span><span id="CONTENTS"></span>内容


-   メディア オブジェクト。 このデバイスは、ストレージ オブジェクト上のフォルダーで、画像、音楽、およびビデオ ファイルを格納します。 前に示したファイルは、1 つのフォルダーが格納されている、デバイスは、(、イメージ フォルダー、ミュージック フォルダー、ビデオ フォルダーなど) に格納されたメディアの種類別に整理するフォルダーにコンテンツを分割できます。
-   連絡先のオブジェクト。 このデバイスは、アドレス帳サービスの子として (名前、電話番号、アドレス、およびなど) などの連絡先情報を格納します。
-   メッセージ オブジェクト。 このデバイスは、SMS サービスの子として SMS (ショート メッセージ サービス) のメッセージを格納します。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>関連トピック


[**WPD ドライバーの概要**](wpd-drivers-overview.md)

 

 





