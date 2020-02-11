---
title: バグチェック 0x1D4 UCMUCSI_LIVEDUMP
description: UCMUCSI_LIVEDUMP ライブダンプの値は0x000001D4 です。
keywords:
- バグチェック 0x1D4 UCMUCSI_LIVEDUMP
- UCMUCSI_LIVEDUMP
ms.date: 02/07/2020
topic_type:
- apiref
api_name:
- UCMUCSI_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 68ffee3e356c8b6b1c716d3c6f0bc2a4db5861db
ms.sourcegitcommit: cf8f0b13f33dfe97a94c8587f1f6797db24d1746
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075644"
---
# <a name="bug-check-0x1d4-ucmucsi_livedump"></a>バグチェック 0x1D4: UCMUCSI\_LIVEDUMP  

> [!IMPORTANT]
> このトピックはプログラマーを対象としています。 コンピューターの使用中にブルースクリーンのエラーコードが表示された顧客の場合は、「[ブルースクリーンエラーのトラブルシューティング](https://www.windows.com/stopcode)」を参照してください。

UCMUCSI_LIVEDUMP ライブダンプの値は0x000001D4 です。 これは、UcmUcsi クラス拡張でエラーが発生したことを示します。 たとえば、UCSI コマンドがタイムアウトしたか、クライアントドライバーからエラーが返されたために UCSI コマンドを実行できなかったことが原因である可能性があります。

UcmUcsiCx は、含まれている UCSI クラス拡張です。 詳細については、「 [USB タイプ-C コネクタシステムソフトウェアインターフェイス (UCSI) ドライバー](https://docs.microsoft.com/windows-hardware/drivers/usbcon/ucsi)」を参照してください。

## <a name="ucmucsi_livedump-parameters"></a>UCMUCSI\_LIVEDUMP パラメーター

パラメーター | 説明
|---------|--------------|
1 | エラーの種類-以下の値を参照
2 | UCSI コマンド値。
3 | 0以外の場合は、追加情報へのポインター。 `dt UcmUcsiCx!UCMUCSICX_TRIAGE` を使用してを表示します。
4 | 予約済み。

**エラーの種類**

0x0: ファームウェアがコマンドに応答しなかったため、UCSI コマンドがタイムアウトしました。

0x1: クライアントドライバーがエラーを返したか、ファームウェアがエラーコードを返したため、UCSI コマンドを実行できませんでした。

## <a name="see-also"></a>参照

[USB チームブログ-UCSI ファームウェアエラーのデバッグ](https://techcommunity.microsoft.com/t5/microsoft-usb-blog/debugging-ucsi-firmware-failures/ba-p/283226)

[ユニバーサル シリアル バス (USB)](https://docs.microsoft.com/windows-hardware/drivers/usbcon/)
