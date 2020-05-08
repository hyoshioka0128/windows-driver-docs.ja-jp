---
title: ウォール クロックとリンク位置のレジスタ
description: ウォール クロックとリンク位置のレジスタ
ms.assetid: 6764affc-a4f0-4568-aa27-7f12e86b818b
keywords:
- ウォールクロックが WDK オーディオを登録する
- リンク位置での WDK オーディオの登録
- HD オーディオ、ウォールクロックレジスタ
- High Definition Audio (HD audio)、ウォールクロックレジスタ
- HD オーディオ、リンク位置レジスタ
- High Definition Audio (HD audio)、リンク位置レジスタ
- 時計 WDK オーディオ、HD オーディオ
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d206f2a04c487f7f847e1505e31fd0fc6a3807b
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925623"
---
# <a name="wall-clock-and-link-position-registers"></a>ウォール クロックとリンク位置のレジスタ


HD オーディオコントローラーには、HD オーディオリンクのビットクロックレートで増加し、約89秒ごとにロールオーバーする32ビットのウォールクロックのカウンターレジスタが含まれています。 ソフトウェアは、デバイスのハードウェアクロック間の相対的なずれを測定することで、このカウンターを使用して2つ以上のコントローラーデバイスを同期します。

さらに、HD オーディオコントローラーには、一連のリンク位置登録が含まれています。 各 DMA エンジンには、エンジンが HD オーディオリンクを介して送信しているデータの現在の読み取りまたは書き込みの位置を示すリンク位置登録があります。 位置レジスタは、現在位置を、循環バッファーの先頭からのバイトオフセットとして表します。

-   レンダーストリームでは、リンク位置レジスタは、DMA エンジンがコーデックへのリンクを介して送信する次のバイトの循環バッファーオフセットを示します。

-   キャプチャストリームでは、リンク位置レジスタは、DMA エンジンがリンクを介してコーデックから受信する次のバイトの、循環バッファーオフセットを示します。

循環バッファーオフセットは、単に、循環バッファーの先頭からの現在の読み取り位置または書き込み位置のバイト単位のオフセットです。 バッファーの末尾に達すると、バッファーの先頭に位置がラップされ、循環バッファーオフセットが0にリセットされます。 循環バッファーはシステムメモリに存在します。 詳細については、 [INTEL HD audio](https://www.intel.com/content/www/us/en/standards/intel-standards-and-initiatives.html) web サイトの「 *Intel High Definition audio Specification* 」を参照してください。

カーネルモードの関数ドライバーは、ウォールクロックとリンク位置のレジスタを直接読み取ることができます。 直接アクセスを有効にするために、HD オーディオバスドライバーは、レジスタを含む物理メモリをシステム仮想メモリにマップします。 関数ドライバーは、 [**GetWallClockRegister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_wall_clock_register)または[**getlinkpositionregister**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/nc-hdaudio-pget_link_position_register)ルーチンを呼び出して、ウォールクロックレジスタまたはリンク位置登録へのシステム仮想アドレスポインターを取得します。 これら2つのルーチンは、HD Audio DDI の両方のバージョンで使用できます。

HD オーディオコントローラーハードウェアは、ウォールクロックとリンク位置を、コントローラー内の他のレジスタを含まないメモリページに登録します。 このため、関数ドライバーがミラー化されたウォールクロックまたは位置レジスタをユーザーモードにマップしている場合、ユーザーモードのプログラムは、コントローラーのその他のレジスタにアクセスできません。 このドライバーでは、ユーザーモードプログラムがこのような他のレジスタをタッチしてハードウェアをプログラムすることを許可することはありません。

登録ミラーリングは、ホストプロセッサのページサイズに対応している必要があります。 ホストプロセッサのアーキテクチャによっては、一般的なページサイズが4096または8192バイトになることがあります。

 

 




