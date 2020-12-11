
## Upload file with storage
```
if ($request->hasFile('original_pic')) {
    $original_pic = $request->file('original_pic');

    $file_extension=$original_pic>getClientOriginalExtension();
    $filename = time() . '.' . $file_extension;

    # upload original image
    Storage::put('ArticlesImages/' . $filename, (string) file_get_contents($original_pic), 'public');

    # croped image from request.
    $image_parts = explode(";base64,", $request->input('article_image'));
    $image_base64 = base64_decode($image_parts[1]);

    Storage::put('ArticlesImages/croped/' . $filename, (string) $image_base64, 'public');

    # get image from s3 or local storage.
    $image_get = Storage::get('ArticlesImages/croped/' . $filename);

    # resize 50 by 50 1x
    $image_50_50 = Image::make($image_get)
            ->resize(340, 227)
            ->encode($file_extension, 80);

    Storage::put('ArticlesImages/1x/' . $filename, (string) $image_50_50, 'public');

    $file_url = Storage::url('ArticlesImages/croped/' . $filename);

    return response()->json(['success' => true, 'filename' => $filename, 'file_url' => $file_url], 200);
} 
```
