```HTML
<div class="certifications-container">
<div class="certification">
<a href="https://learn.microsoft.com/api/credentials/share/en-us/KjetilFurs-3628/3DC41FBA975DE8C4?sharingId=E735EEC265D912D0" target="_blank" rel="noopener noreferrer">
<img src="https://learn.microsoft.com/media/learn/certification/badges/microsoft-certified-associate-badge.svg" alt="Microsoft Certified: Azure Administrator Associate" style="width: 100px; height: auto;">
<p>Microsoft Certified: Azure Administrator Associate</p>
</a>
</div>
<div class="certification">
<a href="https://learn.microsoft.com/api/credentials/share/en-us/KjetilFurs-3628/4491891F35838FE6?sharingId=E735EEC265D912D0" target="_blank" rel="noopener noreferrer">
<img src="https://learn.microsoft.com/media/learn/certification/badges/microsoft-certified-expert-badge.svg" alt="Microsoft Certified: Azure Solutions Architect Expert" style="width: 100px; height: auto;">
<p>Microsoft Certified: Azure Solutions Architect Expert</p>
</a>
</div>
</a>
<!-- Add more certifications as needed -->
</div>
```

```CSS
.certifications-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    align-items: flex-start;
}

.certification {
    text-align: center;
    margin: 10px;
    flex-basis: 20%; /* Default for larger screens */
}

.certification img {
    width: 100px;
    height: auto;
    display: block;
    margin: 0 auto;
}

.certification p {
    margin-top: 10px;
    color: #333;
    font-size: 16px;
}

/* Media query for mobile devices */
@media (max-width: 768px) {
    .certifications-container {
        justify-content: center; /* Center items to handle single column layout better */
    }

    .certification {
        flex-basis: 90%; /* Makes each certification take almost full width of the screen */
        margin: 10px 5%; /* Reduces margin and centers the content */
    }

    .certification img {
        width: 80px; /* Slightly smaller images on mobile */
    }

    .certification p {
        font-size: 14px; /* Slightly smaller text on mobile */
    }
}
```