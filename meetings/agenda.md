# Next Technical Steering Committee Meeting Agenda

- Date: 2022-03-07
- Time: 19:00 UTC

Please file pull requests to add, or discuss items to add, to the agenda.

## Items to Discuss

- Phone number validation as performed by `laminas-I18n` attracts not-too-infrequent issues around correct validation of phone numbers. This was noted in [`laminas-I18n`#74](https://github.com/laminas/laminas-i18n/issues/74). I've put together an initial component at [`gsteel/laminas-i18n-phone-number`](https://github.com/gsteel/laminas-i18n-phone-number), that leverages [`giggsey/libphonenumber-for-php`](https://github.com/giggsey/libphonenumber-for-php) to perform validation and filtering _(Potentially useful view helpers too)_, for possible addition to the Laminas org.<br>From a maintenance perspective, the relatively frequent meta-data updates provided by the `libphonenumber` port should keep it to a minimum 🤞.
