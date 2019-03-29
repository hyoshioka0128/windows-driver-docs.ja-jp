---
title: Windows 98 Core コンポーネント
description: Windows 98 Core コンポーネント
ms.assetid: 59e2c077-c6f5-4965-891b-4601623ca47b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d32b49806477a1b3dcf10cb6bccd73b20a4421cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56571663"
---
# <a name="windows-98-core-components"></a>Windows 98 Core コンポーネント





MIcrosoft Windows 98、静止画像のコア コンポーネントは次の図に示すようにします。

![windows 98 の主要コンポーネントを示す図](images/stiwin98.png)

次の 3 つのコア コンポーネントと通信、サーバー側で*のみ*: *stimon.exe*、 *sti\_ci.dll*、および*sticpl.cpl*. これらのコンポーネントは、それぞれ、静止画像イベント モニタ、クラスのインストーラー、および、スキャナーとカメラのコントロール パネル アプリケーション。 *Sti\_ci.dll*新しい静止画像デバイスがインストールまたは削除するには、ときにのみ呼び出されると*sticpl.cpl*が構成のような作業を行う場合にのみ呼び出されます。

*Stimon.exe*イベントを処理し、通信*のみ*、さらに 1 つと通信する、またはユーザー モードの詳細については、USD1、USD2、および次の図の左側にある USD3 というラベルが付いたドライバー (USDs) を静止画像します。 各ユーザー モード ドライバーは、1 種類のデバイスのバス接続によって、カーネル モード ドライバーと通信します。 ユーザー モードもイメージのドライバーと通信の USB デバイスの*usbscn9x.sys*複合 usb デバイスと*usbscan.sys* noncomposite usb デバイスの SCSI デバイスの場合、ユーザー モード ドライバー両方と通信*scsiscan.sys*と*scsimap.sys*します。

クライアント アプリケーション側では、IHV として上記の図に示されている、TWAIN のデータ ソースを指定する必要があります*vendor.ds*、このコンポーネントの汎用的な名前。 TWAIN データ ソースは、TWAIN スキャン アーキテクチャのコンポーネントでありのインスタンスと通信する*のみ*クライアント側でします。 さらに、*のみ*ユーザー モードの静止イメージ ドライバーと通信 (USD1 図)、前述のカーネル モード ドライバーのいずれかと通信します。

 

 




