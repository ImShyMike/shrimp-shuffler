require_relative './slack'
require_relative './airtable'
require_relative './browser'

def seed_random
  require 'securerandom'
  srand(SecureRandom.random_number(1_000_000))
end

def fetch_and_set_icon(logo)
  logo.download_icon_and_cdn!
  set_icon logo.cdn_url
end

desc "set the ysws thing"
task :ysws do
  logo = Config.get['enable_ysws_fridays'] ? YSWSProgram.top_this_week_with_icon : CommunityLogo.pick_logo
  begin
    fetch_and_set_icon(logo)
  rescue StandardError => e
    Poster.log [
                 'uh oh, we got a problem....',
                 'oh no!',
                 'whoops!'
               ].sample + " hey <@U06QK6AG3RD>: #{e.message}! seems like the bot token stopped working?"
  end
end

desc "set a random community logo!"
task :shuffle do
  seed_random
  # Poster.log [
  #              "it's about that time...",
  #              "hey, it's that time again!",
  #              "guess what time it is?"
  #            ].sample
  logo = CommunityLogo.pick_logo
  begin
    fetch_and_set_icon(logo)
    Poster.logo(logo)
    # Poster.log [
    #              'i think that worked!',
    #              'that oughta do it!',
    #              'done! i think?'
    #            ].sample
  rescue StandardError => e
    Poster.log [
                 'uh oh, we got a problem....',
                 'oh no!',
                 'whoops!'
               ].sample + " hey <@U06QK6AG3RD>: #{e.message}! seems like the bot token stopped working?"
  end
end

task :its_over do
  seed_random
  Poster.log "it's YSWS friday! #{["don't forget to be yourself...", "cya!", "bye..."].sample}"
end

task :were_so_back do
  seed_random
  Poster.log ["now back to your regularly scheduled programming." "we're back!", "we're so back!"].sample
end
