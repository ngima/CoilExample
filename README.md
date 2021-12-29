This repo is just created to resolve the StackOverflow Question: [Coil ImageRequest for drawable resource](https://stackoverflow.com/questions/70476664/coil-imagerequest-for-drawable-resource)


# Implementation

```
package me.ngima.coilexample

import android.content.Context
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import coil.ImageLoader
import coil.request.ImageRequest
import me.ngima.coilexample.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {


    lateinit var binding: ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        binding = ActivityMainBinding.inflate(layoutInflater)

        setContentView(binding.root)

        initListeners()
    }

    private fun initListeners() = with(binding) {
        rdoGroup.setOnCheckedChangeListener { radioGroup, id ->
            when (id) {
                R.id.rdoImage -> updateImage(this@MainActivity, "image")
                R.id.rdoVideo -> updateImage(this@MainActivity, "video")
                R.id.rdoAudio -> updateImage(this@MainActivity, "audio")
                else -> updateImage(this@MainActivity, "file")
            }
        }
    }

    private fun updateImage(context: Context, mimeType: String) {
        val imageLoader = ImageLoader.Builder(context)
            .availableMemoryPercentage(0.25)
            .crossfade(true)
            .build()

        val drawable = when {
            mimeType.startsWith("image") -> R.drawable.ic_baseline_image_24
            mimeType.startsWith("video") -> R.drawable.ic_baseline_ondemand_video_24
            mimeType.startsWith("audio") -> R.drawable.ic_baseline_audiotrack_24
            else -> R.drawable.ic_baseline_attach_file_24
        }

        val imageRequest = ImageRequest.Builder(context)
            .data(drawable)
            .crossfade(true)
            .target(binding.imageView)
            .build()

//blah-blah
// and somewhere deep inside code
        imageLoader.enqueue(imageRequest)
    }
}
```

# Output
<a href="/output/coil_drawable_loading_output.mp4"><img src="/output/coil_drawable_loading_output.gif"/></a>
