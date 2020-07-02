---
title: KSPROPERTY \_ PIN \_ MODEDATAFORMATS
description: クライアントは、KSPROPERTY_PIN_MODEDATAFORMATS プロパティを使用して、pin ファクトリによってインスタンス化された pin のサポートされている各モードでサポートされている形式の一覧を取得します。
ms.assetid: AD028946-2E6C-4385-B336-657FA1743EA8
keywords:
- ストリーミングメディアデバイスの KSPROPERTY_PIN_MODEDATAFORMATS
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_MODEDATAFORMATS
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 07/01/2020
ms.localizationpriority: medium
ms.openlocfilehash: d25a1ddec24f8ddee5e150acaa9f58e89e3cef5a
ms.sourcegitcommit: 7a69c2e0abf91a57407b13a30faf24925f677970
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/01/2020
ms.locfileid: "85835152"
---
# <a name="ksproperty_pin_modedataformats"></a>KSPROPERTY \_ PIN \_ MODEDATAFORMATS

クライアントは、 **Ksk プロパティの \_ pin \_ MODEDATAFORMATS**プロパティを使用して、pin ファクトリによってインスタンス化されたピンのサポートされている各オーディオシグナル処理モードでサポートされている形式の一覧を取得します。

## <a name="usage-summary-table"></a>使用状況の概要テーブル

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>取得</th>
<th>オン</th>
<th>Target</th>
<th>プロパティ記述子の型</th>
<th>プロパティ値の型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>はい</p></td>
<td><p>いいえ</p></td>
<td><p>Assert</p></td>
<td><p>KSP_PIN、その後にモード GUID が続きます。</p></td>
<td><p>KSMULTIPLE_ITEM 構造体の後に一連の<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a>構造体が続きます。</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>Remarks

クライアントは、このプロパティを使用して、pin ファクトリによってインスタンス化されたピンによって、特定のオーディオ信号処理モードでサポートされている形式の一覧を取得します。

[**KSP \_ **](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)を使用してこのプロパティを指定し、その後に mode guid を指定します。ここで、KSP_PIN メンバーとモード guid は、形式の一覧を返すピンファクトリとモードを指定します。

**Ksproperty \_\_MODEDATAFORMATS**を指定すると、サポートされている形式が[**ksk の複数の \_ 項目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksmultiple_item)の構造として返されます。構造体の各項目は、特定の[KSDATAFORMAT 構造体](ttps://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)に対するオフセットを持つ ULONGLONG であり、KSMULTIPLE_ITEM の先頭からの値です。
- KSMULTIPLE_ITEM:: Size 値には、KSMULTIPLE_ITEM のサイズと各 KSDATAFORMAT のサイズが含まれます。 
- KSMULTIPLE_ITEM:: Count 値には、各 KSDATAFORMAT のインデックスの数が含まれます。

ほとんどの場合、返される KSDATAFORMAT 構造体は、実際には KSDATAFORMAT_WAVEFORMATEXTENSIBLE、またはと一致するサイズの[KSDATAFORMAT_WAVEFORMATEX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)構造体になります。

たとえば、2つの形式をサポートする pin ファクトリの値は、次のようになります。

```cpp
{
    // Example Property Value Result, with 2 formats
    // Size of the KSMULTIPLE_ITEM structure + Size of two ULONGLONG offset values + Size of first format + Size of second format
    sizeof(KSMULTIPLE_ITEM) + sizeof(ULONGLONG)*2 + (First KSDATAFORMAT::Size) + (Second KSDATAFORMAT::Size),
    // Number of formats being returned
    2,
    // Offset of the first format from the beginning of the Property Value
    (sizeof(KSMULTIPLE_ITEM) + 2 * sizeof(ULONGLONG)),
    // Offset of the second format from the beginning of the Property Value
    (sizeof(KSMULTIPLE_ITEM) + 2 * sizeof(ULONGLONG) + (First KSDATAFORMAT::Size),
    // First format structure
    {(First KSDATAFORMAT)},
    // Second format structure
    {(Second KSDATAFORMAT)}
}
```

詳細については、「[拡張 Wave 形式記述子](https://docs.microsoft.com/windows-hardware/drivers/audio/extensible-wave-format-descriptors)」を参照してください。

## <a name="supported-mode-format-and-buffer-recommendations"></a>サポートされているモード形式とバッファーに関する推奨事項

Windows 10 バージョン 2004 (20H1) 以降では、サポートされているオーディオ信号処理モードの形式とバッファーサイズの制約を報告するために、 **Ksproperty \_ PIN \_ MODEDATAFORMATS**と[KSAUDIO_PACKETSIZE_CONSTRAINTS2](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)を使用する方法が推奨されています。 このアプローチを使用すると、エンドポイントでサポートされている形式とバッファーサイズを検出するために多数のストリームを作成しなくても、Windows オーディオシステムでエンドポイントのストリーミング機能を効率的に取得できます。

### <a name="requirements"></a>必要条件

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Windows 10 バージョン 2004 (20H1) から使用できます。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ks (Ks を含む)</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>関連項目

[**KSP の \_ PIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

[**KSAUDIO_PACKETSIZE_CONSTRAINTS2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksaudio_packetsize_constraints2)

[KSDATAFORMAT_WAVEFORMATEX](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)  
