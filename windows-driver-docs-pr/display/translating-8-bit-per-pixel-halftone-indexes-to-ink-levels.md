---
title: インク レベルにピクセルあたり 8 ビット ハーフトーン インデックスの変換
description: インク レベルにピクセルあたり 8 ビット ハーフトーン インデックスの変換
ms.assetid: 5859b379-4e03-4cd8-836d-9a0b068b47c0
keywords:
- GDI WDK Windows 2000 の表示、ハーフトーン
- グラフィックス ドライバー WDK Windows 2000 の表示、ハーフトーン
- 描画の WDK GDI、ハーフトーン
- ハーフトーン WDK GDI
- ピクセルあたり 8 ビット CMY マスク モード WDK GDI
- GenerateInkLevels
- INKLEVELS
- WDK GDI ピクセルあたり 8 ビット ハーフトーンを翻訳するインデックスを作成します。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d664d9cc1e4662081bafa86777b8592f347a60b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2019
ms.locfileid: "56558069"
---
# <a name="translating-8-bit-per-pixel-halftone-indexes-to-ink-levels"></a>インク レベルにピクセルあたり 8 ビット ハーフトーン インデックスの変換


## <span id="ddk_translating_8_bit_per_pixel_halftone_indexes_to_ink_levels_gg"></span><span id="DDK_TRANSLATING_8_BIT_PER_PIXEL_HALFTONE_INDEXES_TO_INK_LEVELS_GG"></span>


**GenerateInkLevels**ここで示すように関数がインク レベルにピクセルあたり 8 ビット ハーフトーン インデックスに変換する方法の例を示します。 CMY モードと CMY でこれらのインデックスが含まれている\_その GDI のモードのパレットを反転[ **HT\_Get8BPPMaskPalette** ](https://msdn.microsoft.com/library/windows/hardware/ff567320)関数で返しますその*pPaletteEntry*パラメーター。 **GenerateInkLevels** INKLEVELS 構造体の 256 要素の配列を生成します。

この関数を使用して、Windows 2000 CMY モードまたは windows 2000 以降 CMY のいずれかを生成することができます\_反転モード変換テーブル。 この関数は、Windows 2000 CMY モード CMY332 リバース マッピング インデックス テーブルを生成することも使用できます。 (CMY332 に、シアン、マゼンタ、および黄色の 2 つのビットのある 3 つのビットが使用) します。ときに*CMYMask*値は 3 ~ 255 の範囲で、関数の呼び出し元は、このテーブルを使用して、windows 2000 以降 CMY をマップする\_現在既存の Windows 2000 CMY インデックスにインデックスを反転ドライバー。

### <a name="span-idinklevelsstructurespanspan-idinklevelsstructurespaninklevels-structure"></a><span id="inklevels_structure"></span><span id="INKLEVELS_STRUCTURE"></span>INKLEVELS 構造体

```cpp
typedef struct _INKLEVELS {
   BYTE  Cyan;          // Cyan level from 0 to max
   BYTE  Magenta;       // Magenta level from 0 to max
   BYTE  Yellow;        // Yellow level from 0 to max
   BYTE  CMY332Idx;     // Original windows 2000 CMY332 Index
} INKLEVELS, *PINKLEVELS;
```

### <a name="span-idexamplegenerateinklevelsfunctionspanspan-idexamplegenerateinklevelsfunctionspanexample-generateinklevels-function"></a><span id="example_generateinklevels_function"></span><span id="EXAMPLE_GENERATEINKLEVELS_FUNCTION"></span>GenerateInkLevels 関数の例

**GenerateInkLevels**関数は、ピクセルあたり 8 ビットの翻訳テーブル内の値に基づいて、INKLEVELS 構造体の計算、 *CMYMask*と*CMYInverted パラメーター*. この関数は、有効なは、INKLEVELS 変換のテーブルを生成*CMYMask* 0 ~ 255 の範囲の値。

この関数が呼び出されたときに、 *pInkLevels*パラメーターは、256 INKLEVELS エントリの有効なメモリ位置を指す必要があります。 関数が返した場合**TRUE**、し*pInkLevels*インク レベルでは、ピクセルあたり 8 ビットのインデックスを変換する、または古い CMY332 インデックスにマップするために使用できます。 関数を呼び出すと*CMYMask*値が無効です (0 シアン、マゼンタ、黄色レベルのいずれかの 255 ~ 3 の値) に設定すると、関数を返します**FALSE**します。

```cpp
BOOL
GenerateInkLevels(
    PINKLEVELS  pInkLevels,  // Pointer to 256 INKLEVELS table
    BYTE        CMYMask,     // CMYMask mode
    BOOL        CMYInverted  // TRUE for CMY_INVERTED mode
    )

{
    PINKLEVELS  pILDup;
    PINKLEVELS  pILEnd;
    INKLEVELS   InkLevels;
    INT         Count;
    INT         IdxInc;
    INT         cC;  // Number of Cyan levels
    INT         cM;  // Number of Magenta levels
    INT         cY;  // Number of Yellow levels
    INT         xC;  // Max. number Cyan levels
    INT         xM;  // Max. number Magenta levels
    INT         xY;  // Max. number Yellow levels
    INT         iC;
    INT         iM;
    INT         iY;
    INT         mC;
    INT         mM;

    switch (CMYMask) {

    case 0:

        cC =
        cM =
        xC =
        xM = 0;
        cY =
        xY = 255;
        break;

    case 1:
    case 2:

        cC =
        cM =
        cY =
        xC =
        xM =
        xY = 3 + (INT)CMYMask;
        break;

    default:

        cC = (INT)((CMYMask >> 5) & 0x07);
        cM = (INT)((CMYMask >> 2) & 0x07);
        cY = (INT)( CMYMask       & 0x03);
        xC = 7;
        xM = 7;
        xY = 3;
        break;
    }   // end switch statement

    Count = (cC + 1) * (cM + 1) * (cY + 1);

    if ((Count < 1) || (Count > 256)) {
        return(FALSE);
    }

    InkLevels.Cyan      =
    InkLevels.Magenta   =
    InkLevels.Yellow    =
    InkLevels.CMY332Idx = 0;
    mC                  = (xM + 1) * (xY + 1);
    mM                  = xY + 1;
    pILDup              = NULL;
    if (CMYInverted) {

        //
        // Move the pInkLevels to the first entry following 
        // the centered embedded entries.
        // Skipped entries are set to white (zero). Because this 
        // is a CMY_INVERTED mode, entries start from back of the
        // table and move toward the beginning of the table.
        //

        pILEnd      = pInkLevels - 1;
        IdxInc      = ((256 - Count - (Count & 0x01)) / 2);
        pInkLevels += 255;

        while (IdxInc--) {

            *pInkLevels-- = InkLevels;
        }

        if (Count & 0x01) {

            //
            // If we have an odd number of entries, we need to
            // duplicate the center one for the XOR ROP to
            // operate correctly. pILDup will always be index
            // 127, and the duplicates are at indexes 127 and 128.
            //
            pILDup = pInkLevels - (Count / 2) - 1;
        }

        //
        // We are running from the end of table to the beginning,
        // because in CMY_INVERTED mode, index 0 is black and
        // index 255 is white. Since we generate only Count 
        // white, black, and colored indexes, and place them at
        // the center, we will change xC, xM, xY max. indexes 
        // to the same as cC, cM and cY
        // so we only compute cC*cM*cY entries.
        //

        IdxInc = -1;
        xC     = cC;
        xM     = cM;
        xY     = cY;

    } else {
        IdxInc = 1;
        pILEnd = pInkLevels + 256;
    }

    //
    // In the following composition of ink levels, the index
    // always runs from 0 ink level (white) to maximum ink 
    // levels (black).  With CMY_INVERTED mode, we compose ink
    // levels from index 255 to index 0 rather than from index 
    // 0 to 255.
    //

    if (CMYMask) {

        INT Idx332C;
        INT Idx332M;

        for (iC = 0, Idx332C = -mC; iC <= xC; iC++) {

            if (iC <= cC) {

                InkLevels.Cyan  = (BYTE)iC;
                Idx332C        += mC;
            }

            for (iM = 0, Idx332M = -mM; iM <= xM; iM++) {

                if (iM <= cM) {

                    InkLevels.Magenta  = (BYTE)iM;
                    Idx332M           += mM;
                }

                for (iY = 0; iY <= xY; iY++) {

                    if (iY <= cY) {

                        InkLevels.Yellow = (BYTE)iY;
                    }

                    InkLevels.CMY332Idx = (BYTE)(Idx332C + 
                                          Idx332M) +
                                          InkLevels.Yellow;
                    *pInkLevels         = InkLevels;

                    if ((pInkLevels += IdxInc) == pILDup) {

                        *pInkLevels  = InkLevels;
                        pInkLevels  += IdxInc;
                    }
                }
            }
        }

        //
        // Now, if we need to pad black at the other end of the
        // translation table, then do it here. Notice that
        // InkLevels are at cC, cM and cY here and CMY332Idx
        // is at black.
        //

        while (pInkLevels != pILEnd) {

            *pInkLevels  = InkLevels;
            pInkLevels  += IdxInc;
        }

    } else {

        //
        // Gray Scale case
        //

        for (iC = 0; iC < 256; iC++, pInkLevels += IdxInc) {

            pInkLevels->Cyan      =
            pInkLevels->Magenta   =
            pInkLevels->Yellow    =
            pInkLevels->CMY332Idx = (BYTE)iC;
        }
    }

    return(TRUE);
}
```

 

 





